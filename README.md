# InterView: Demonstrating a framework to support interaction-driven visualization systems design
InterView is implemented in a system, composed of two software components, one to automatically generate the interaction space of a visualization system using a statechart, and one to automatically replay user traces, reproducing each low-level interaction an end user performed in the interaction log. To demonstrate the capabilities of InterView, we applied it to a well-known crossfilter interface, Falcon, to guide the visualization system designers in discovering the root causes behind excessive latency, coupled with a complete understanding of the interaction space of their visualization system. In such a way, designers can finally acknowledge the problems of their visualization system with higher granularity and precision, also giving more context to the feedback received by the end users. 

## Demonstration Video

A demonstration video of InterView is present in the root directory of this repository, named "demonstration.mp4":

https://github.com/MatteoFilosa/InterView/assets/67047355/c5404977-f9ae-443f-8459-8b028254deb2


## Installation

### Steps to run the server for the first time:

1) Install the requirements running "pip install -r requirements.txt" (If you don't have pip installed, install it)

2) Create a virtual environment by running the command "python -m venv <name_of_the_virtual_environment>" in the terminal

3) Run the runApp file contained in the main directory to start the app: python runApp.py <name_of_the_virtual_environment>

InterView: installation of the dependencies for the traces replay and state chart generation features

1) Install selenium 4.1.3 ----> pip install selenium==4.1.3 (it should be already installed from step 1)

2) Download and put in any folder you like an updated chromedriver https://googlechromelabs.github.io/chrome-for-testing/#stable (Find the list here and download the version relative to your OS). Don't forget to update Chrome.

3) Add the chromedriver's path to PATH environmental variable

4) Change line 1143 in PathSimulator.py to your path to chromedriver. Use double '\' for the path if you get a syntax error.

5) Install the next node modules:

- NodeJS (from v12.20.2)
- Puppeteer node module v13.7.0 (npm install puppeteer@13.7.0)
- fs node module v1.0.0 (npm install fs@v1.0.0)
- is-same-origin node module v0.0.7 (npm install is-same-origin@v0.0.7)

## InterView: main functionalities and how to run them

1) In the static/files/URLs folder there's the sampleUrls file. Copy a URL from the file and put it in the "Load System" placeholder: the visualization system will be loaded on the left, the resulting state chart will be loaded on the right. The URLs contain precomputed state charts. If for a visualization system a state chart wasn't generated, the system will invoke a subprocess that in the end generates it and puts it in the DB (it is the state chart generation subprocess). This subprocess can take much time, even an entire day, keep that in mind while trying to generate a new state chart

2) In the User Traces Tab you can see all user traces captured, with many details such as violations in latency thresholds, interactions, etc. They are relative to the Falcon crossfilter Visualization system (see https://vega.github.io/falcon/flights/). 

3) By selecting a single trace, an extra info div appears on the right. On the top right corner, there's a button for seeing the user trace (or traces) in the interaction space (state chart), whose edges' label are colured accordingly to a color scale, indicating how much a certain interaction has been performed or not. If the trace recorded violations in latency thresholds, it is also possible to see them reflected in the state chart.

4) At the bottom of the extra info for the trace, it is possible to see a button, used to invoke the replay functionality (available only for a single trace). A new window will be opened, and the trace will be replayed, doing the same interactions in the trace, seeing on the left the visualization system and on the right the state chart, that is coloured basing on the interaction that is being performed in the visualization system. It is possible to play, pause, stop, and reproduce directly the next event by playing the relative buttons on the top.

