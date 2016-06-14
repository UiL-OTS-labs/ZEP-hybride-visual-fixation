# Hybrid Visual Fixation Experiment

The hybrid visual fixation or habituation (`hvf`) can be used to access perception in younger children. It involves measuring looking times via scoring a video feed of the child. This experiment has been programmed as requested by [Maartje de Klerk][maartje] by [Chris van Run][chris].

# Parts
There are two main parts.
- Attention testing :- assesses the current attention span of the participant.
- Fixation testing :- assesses the amount of fixation on certain auditive tokens.

These are presented in four phases:
- Pre-test phase (attention testing)
- Habituation phase (fixation testing)
- Test phase (fixation testing)
- Post-test phase (attention testing)

# Input
The `stimuli` directory contains are csv files which are used for the fixation testing. Other stimuli are defined in the `stimuli.zm` module in `./modules`, `./test` and `./attention_test` directories. The other input is gathered from the `global_defs.zm` and `defs.zm` modules. The name of the input-csv files are expected to be build from the three determinators that are present in the participant data: 
* contrast (native/nonnative)
* first alteration (alt/nalt)
* and token (fep/fap). 

Furthermore each list needs to be in a test and habitiuation version (prefix: 'hab_' or 'test_'). Examples are: `test_native_alt_fep.csv` or `hab_native_nalt_fap.csv`.

# Output
One can get output by running `zepdbextract` in the experiment directory. This generates the following tables.

*Every look*
* hvf-01-pre_test_attention-1.csv
* hvf-01-habituation-1.csv
* hvf-01-test-1.csv
* hvf-01-post_test_attention-1.csv

*Every look collapsed/summised per trial*
* hvf-01-summary_habituation-1.csv
* hvf-01-summary_post_test_attention-1.csv
* hvf-01-summary_pre_test_attention-1.csv
* hvf-01-summary_test-1.csv

*Inclusion criteria per particpant (minimum habituation and minimum attention)*
* hvf-01-inclusion_variable_summary-1.csv

# Requirements
- Zep installed. (From [here][beexy-zep-download] for instance)
- This experiment unarchived.
- A camera to record particpant.
- A method to overlay the camera stream with the control window.
- A BeexyBox response box or for less accurate looktime measurements: a keyboard.

# Running the experiment
- Navigate via the CLI/CMD to the folder or run `linux-terminal.sh` / `windows-terminal.bat`.
- Run the command `zep hvf.zp`.
- Create a participant and enter participant data via the control window.
- Press `start`.

[beexy-zep-download]: <http://beexy.org/zep/wiki/doku.php?id=download>
[maartje]: <http://www.uu.nl/staff/MdeKlerk/0>
[chris]: <http://www.uu.nl/staff/CPAvanRun>