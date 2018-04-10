# Hybrid Visual Fixation Experiment

The hybrid visual fixation or habituation (`hvf`) can be used to access perception in younger children. It involves measuring looking times via scoring a video feed of the child. This experiment has been programmed as requested by [Maartje de Klerk][maartje] by [Chris van Run][chris] and later on by Jacco van Elst.

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
* group (one or two)

Determined by a *combination of contrast and group* as filled out in the participant GUI, a certain token is selected (A1/A2/B1/B2). If the contrast is nonnative a type A token is selected, and if nonnative, a type B token. Which one of the two versions is habituated and then tested with alternations, depends on group_one_two.



The following participant info is relevant for the study:

Name                       | Description                              | Valid choices           | Comments
---------------------------|------------------------------------------|-------------------------|-----------------------------------------------------------------------------------------------
participant ID             | Some name or code                        | Baby1, B017, etc.       |
created                    | ISO time stamp                           | 2023-03-14 03:14:59     | Automatically filled
gender_m_f                 | Gender                                   | "m" or "f"              |
age_months                 | Age in months                            | All integers above 0    | Careful with this value
type_risk_control          | Wether subject is 'special'              | "risk" or "control"     | E.g. dyslexia in family
contrast_native_nonnative  | Are both sounds native?                  | "native" or "nonnative" | If native, select A tokens, otherwise B!
first_alternation_alt_nalt | Wether the first trial alternates or not | "alt" or "nalt"         | If "nalt", the first trial does not alternate, but the second does. And vice versa.
group_one_two              | Deternines which token is trained/tested | "one" or "two"          | I.e.: train on "faap" and contrast with "feep", or vice versa. (native example, given Dutch language).

# CSV file names and contents in relation to the current experiment goal

Each file name needs to be in a test or a habitiuation version (prefix: 'hab_' or 'test_').Examples are: `test_native_alt_A1.csv` or `hab_B2.csv`. *Test type* csv files contain two sounds that are contrasted, *habituation type* files contain. In our current operationalisation, the "not on first token altenating" only determines wether **the first pair of tokens** is a real contrast or not. So, for testing, an "alt" .csv in the current operationalisation implies contrasts on id 1, 5, 8 and 12, whereas "nalt" implies contrasts on id 2, 5, 8 and 12.

# Tokens, speakers and trials (specific)
In the current setup, 4 speakers have been recorded, reading the tokens aloud. Of one speaker, multiple versions of the same token are used in the testing phase, so we have the same voice, reading the token aloud a bit differently. In this operationalisation, sound file names in the .csv file contents like "feep1.wav" and "feep5.wav" imply: token "feep", the *same voice*, *different versions*.

example:


#### Habituation on "feep" token
feep1 = sound 'feep' by speaker 1

id | sound 1 | sound 2
---|---------|---------
1  | feep1   | feep1
2  | feep2   | feep2
3  | feep3   | feep3
... (etc. until habituated. Version 5 is not used during habituation)

Ie.: for each token in the list, a trial consists of a tuple of identical speech sounds, made by the same speaker (voice).

#### Testing contrasts with "feep" token ("faap").
In the testing phase, a different flow starts. Let's say this is a "nalt" version. Here, *version 5* is *new* to the participant, so the contrast is either on token, or on version, with the newest always presented first in the trial tuple.

id | sound 1    | sound 2   | extra (not in .csv) 
---|------------|-----------|-------------------------------------------------------------------------------- 
1  | feep5      | feep1     | 'feep' version 5 has never been heard before 
2  | f**aa***p5 | feep**5** | both versions are 'new', the first *actual* contrast in terms of tokens
3  | feep5      | feep1     |
4  | feep5      | feep1     |
5  | f**aa**p5  | feep5     | alternation (token contrast) on 5
6  | feep5      | feep1     |
7  | feep5      | feep1     |
8  | f**aa**p5  | feep5     | alternation on 8
9  | feep5      | feep1     |
10 | feep5      | feep1     |
11 | feep5      | feep1     |
12 | f**aap**5  | feep5     | alternation on 12

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
- Use the response box to continue and mark looking time onset/offset. (Note: keyboard alternatives are `t` for looking time and `spacebar` for continue)
[beexy-zep-download]: <http://beexy.org/zep/wiki/doku.php?id=download>
[maartje]: <http://www.uu.nl/staff/MdeKlerk/0>
[chris]: <http://www.uu.nl/staff/CPAvanRun>