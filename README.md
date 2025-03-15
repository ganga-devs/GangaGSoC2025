# Evaluation for Ganga projects in GSoC 2025

The evaluation that forms part of the Ganga projects in GSoC is divided up into three pieces, but most of you will only do two of them.

1) A part that demonstrates a basic proficiency in Ganga and the ability to work with Python (this is compulsory)
2) Demonstration that you can integrate communication with an LLM from inside a python script (do this if interested in the LLM project)
3) Demonstration that you can perform a static analysis of a code base in a testing environment (do this if interested in the deprecation project)
   
## Setup
Following the steps below will ensure that you can work freely on your project, can submit code through pushing it to GitHub but at the same time keep it private. Please avoid making your repository public as we want each student to work on this independently.

- Create a duplicate of the repository following the [instructions](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository). Then make that duplicate private. Please do not make a normal fork as that will then prevent you from making the repository private.
- Give the GitHub users `egede`, `alexanderrichards`, `mesmith75` access to your repository as collaborators.

For performing actual work for the challenge you need to work within a linux environment. This can be either as a native linux machine, on a virtual machine or using WSL. While recommending python 3.13 or 3.12, everything should work back to version 3.8. To setup the working environment, we suggest to use a virtual environment in the follwing way:

```bash
python3 -m venv GSoC
cd GSoC/
. bin/activate
python -m pip install --upgrade pip wheel setuptools
python -m pip install -e git+https://github.com/YOUR-GITHUB-USERNAME-HERE/GangaGSoC2025#egg=gangagsoc
```

Through the dependency, this will install Ganga as well, such that you can work with it directly inside the virtualenv.

## Communication

Communication is an important part of working in GSoC. We use the CERN Mattermost server for instant messaging about the project. Please
- Create a CERN guest account by following the [instructions](https://users-portal.web.cern.ch/guest-registration)
- Follow [the link](https://mattermost.web.cern.ch/signup_user_complete/?id=6t4p1zptyp8pdn6ptore9ex9hw) to
  join the Ganga Team in MatterMost. You can install MatterMost as an application, or you can just use it inside your browser.
- When you have joined the Ganga Team, please join the [GSoC2025 channel](https://mattermost.web.cern.ch/ganga/channels/gsoc-2025).
- Introduce yourself with a few words to the channel.

It is by far the best if most communication is public in the MatterMost channel, but you can also instant message @egede, @masmith and @arichard for more specific issues. Please do not post solutions to the challenge to the public channel but you are welcome to discuss issues regarding the challenge.

## Completing evaluation

To complete the challenge you should push everything to the main branch of your forked repository. In the repository, we expect
- That the [setup.py](setup.py) file is updated with any extra `python` package dependencies that you may have introduced.
- Update the file [PROJECT.md](PROJECT.md) to document what you have done and how we can test it. You can also include images or short screen grabbed movies that illustrate functionality.
- A file CV.pdf that contains your CV.
- That you have implemented tests of the code that can be tested with running `python -m pytest` to illustrate that everything works as expected. Tests should be placed in the directory `test` and have self-explaining names.

## Ganga initial task (this is compulsory)

Start by performing this task.

1) Demonstrate that you can run a simple `Hello World` Ganga job that executes on a `Local` backend.
2) Create a job in Ganga that demonstrates splitting a job into multiple pieces and then collates the results at the end.
  - Use the included file `LHC.pdf`.
  - Create a job in Ganga that in python (or through using system calls) split the pdf file into individual pages. 
  - Create a a second job in Ganga that will count the number of occurences of the word "it" in the text of the PDF file. It should be counted whether it is capitalised or not. Make sure not to count other words that have the letters "it" inside them. So "It is best when it uses Ganga" should have a count of two, while "The initial test did no work" should have a count of zero.
  - Using the `ArgSplitter` create subjobs that each will count the occurences for a single page.
  - Create a merger that adds up the number extracted from each page and places the total number into a file.
 3) Create test cases that demonstrate what you have done and that it is working. In the `test` directory you will find an example of a trivial test. All tests can be executed by `python -m unittest` when executed from the `gangagsoc` directory. To make tests that include Ganga objects, be inspired by tests in [existing tests](https://github.com/ganga-devs/ganga/blob/develop/ganga/GangaCore/test/GPI/TestArgSplitter.py). Note the use of `sleep_until_completed`.
 4) Confirm that your new tests are running successfully within the defined GitHub action. Click on "Actions" in the web interface of your repository. The tests will run each time you push a file to the "main" branch.

## Interfacing Ganga (do this if interested in the LLM project)

The purpose of this challenge is to demonstrate that you can communicate with a Large Language Model in a programmatic way. Which LLM you use is for you to decide and the performance of the LLM itself (in terms of the quality of the replies) is irrelevant.

1) Create code that sets up a conversation with an LLM of your choice.
2) Craft a set of questions to the LLM that will make it write code that can execute a job in Ganga that will calculate an approximation to the number pi using an accept-reject simulation method will one million simulations. The job should be split into a number of subjobs that each do thousand simulations.
3) Write a test that executes the proposed code. The test should succeed if the test tries to execute the code in Ganga. It doesn't matter if the code proposed by the LLM works.
4) Create a Django app that when running will accept questions, use the LLM of choice and provide the answer from the LLM. No requirement to keep knowledge of prior questions. Also no security concerns, it can just be implemented with `http` to a `localhost` port. Create a small screen grabed movie or a set of screenshots to illustrate the use.

## Static analysis of a code base in a testing environment (do this if interested in the deprecation project)

1) Write code that will perform a static analysis of the code located in the `deprecated` test directory and identify decorators of the type
```
@deprecated(version='8.6.9', reason="Singularity is the old name, use Apptainer instead", expiry=datetime.date(2024,7,1))
```
   where todays date is after the expiry time. Code that is commented out should not be considered.

2) Integrate this into the continuous integration such that a failure is reported if there are deprecated functions that have not been removed before their expiry.
3) Create screen grabs or similar to document how it is working.

## Feedback on challenge
You are welcome to seek feedback on your solution to the challenges while they are still work in progress. For feedback PM @egede, @masmith and @arichard in MatterMost. Make sure that you have given access in Github to us as directed above.

## Submission
When you are ready and have the final version of your code in the main branch of your repo, then please use the [Google form](https://docs.google.com/forms/d/e/1FAIpQLScCrQBFrm0auXYJqKuzDGkjoHdj-fV7hvo_TKBc85nJpIIY1A/viewform) to let us know.
