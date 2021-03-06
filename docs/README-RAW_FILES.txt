
                        README - RAW FILES

                        Author: Tyson Reimer
                        Date: October 21st, 2019

This file discusses the raw .txt files that comprise the dataset.

-------------------------------------------------------------------------------
-------------------------------------------------------------------------------

                            SECTION I: File Names

The raw .txt files that comprise the dataset can be found within the
folders found in:

/UM-BMID/scan-data/{gen-one, gen-two}/raw/

These files are generated by the software program used to control the
pre-clinical system at the University of Manitoba during a scan.

The raw file names are in the format:

<Mono, Multi>_<expt str>_(<faW, foC>_z0_a<lift stage position>_l72)_<date>.txt

The following describes each component:

    <Mono, Multi>
        Indicates whether the data was from the Port A antenna (Mono),
        in which case the file contains S11 measurements, or from the
        Port B antenna (Multi), in which case the file contains S21
        measurements.

        Mono = S11
        Multi = S21

    <expt_str>
        This is a string that is unique to that experiment, typically
        it is 'exptXX' where XX is the number of the experiment from
        the session in which it was measured

    <faW, foC>
        Indicates whether the scan was completed with the antennas
        rotating clockwise or counter-clockwise. If faW, the scan was
        performed clockwise. If foC, the scan was performed
        counter-clockwise.
        **NOTE: In all clean files, data from all scans are converted
                so that the first column of the array contains the
                measurements from the first antenna position, and the
                Nth column contains the measurements from the Nth
                position, **as if the antenna was rotating clockwise**.

    <lift stage position>
        The relative lift stage position. Typically 2000k or 2100k.
        These values cannot be converted directly into distances
        because they are relative to the calibration performed.
        **NOTE:
            The height of the antennas during each scan is recorded as
            part of the scans metadata, under the string 'ant_height'.

    <date>
        The time and date stamp, when the file was saved.

-------------------------------------------------------------------------------
-------------------------------------------------------------------------------

                    SECTION II: File Data Format

The raw .txt files contain comma-separated-values arranged into rows and
columns.

Each row contains the frequency-domain measurements of either the real
or imaginary parts of the S-parameter. The first, third, etc., rows
contain the *real* parts of the parameters, while the second, fourth,
etc., rows contain the *imag* parts of the parameters.

The first and second rows contain the complete S-parameter measurements
from the *first* antenna position in the scan. The third and fourth rows
contain the measurements from the *second* antenna position, and so on.

Notes:

    - If there are 2N rows in the txt file, then N antenna positions
      were used in the scan.
        **NOTE: All scans in UM-BMID were performed using 72 antenna
                positions.

    - The value in the Nth row and the Cth column of the file contains
      the measured *real* part of the S-parameter, if N is odd
      (assuming 1-based indexing), or the measured *imag* part
      if N is even, at the Cth frequency at the (N // 2) * 72 antenna
      position.
