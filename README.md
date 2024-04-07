# InterView: Demonstrating a framework to support interaction-driven visualization systems design
InterView is implemented in a system, composed of two software components, one to automatically generate the interaction space of a visualization system using a statechart, and one to automatically replay user traces, reproducing each low-level interaction an end user performed in the interaction log. To demonstrate the capabilities of InterView, we applied it to a well-known crossfilter interface, Falcon, to guide the visualization system designers in discovering the root causes behind excessive latency, coupled with a complete understanding of the interaction space of their visualization system. In such a way, designers can finally acknowledge the problems of their visualization system with higher granularity and precision, also giving more context to the feedback received by the end users. 

## Demonstration Video

A demonstration video of InterView is present in the root directory of this repository, named "demonstration.mp4":

https://github.com/MatteoFilosa/InterView/assets/67047355/ec493b63-0cb8-4878-878a-069461c7a1ed


## Usage

### Statechart Generator
Inside the ./statechart-generator folder there is the **Statechart Generator** software component.
In order to build and run it in your machine, you must have already installed and configured:

    NodeJS v12.20.2
    Puppeteer node module v13.7.0
    fs node module v1.0.0
    is-same-origin node module v0.0.7

Then you can open a terminal inside that folder and run the main.js file with NodeJS. You can specify the link to the visualization inside the ./statechart-generator/material/system_url.txt configuration file, while the list of excluded events can be customized inside the ./statechart-generator/material/excluded_events.txt configuration file.


Inside /validations/statecharts there are the generated Complete Statecharts of eleven visualization systems:

	1. Falcon
	2. DataVis
	3. Crumbs
	4. Crosswidget
	5. Ivan
	6. Nemesis
	7. IDMVis
	8. Wasp
	9. Radviz
	10. InfluenceMap
	11. Nemesis
	

### Traces Replayer

Inside the ./traces-replayer folder there is the **Traces Replayer** software component.

The script automatically explores Falcon's 7 million flights visualization (whose url is contained in "conf.json") given a sample logged trace name "exploration_falcon_7M_1.json". Other explorations can be found in the "explorations" folder. To test the other explorations, remember to change line 1134, inputing the desired user trace's name to test. The replay returns as output three files: a "summary_falcon_7M.json" file in the count folder, another "summary_falcon_7M.json" file in the times_and_violations folder (different from the previous one, containing all the times each interaction required to be reproduced), an additional "summaryProblems_falcon_7M.json" file that contains the violations found in the given trace.

All the first two types of files were already computed in the "count" and "time_and_violations" folder for the 50 traces collected in our previous work.
The count.py and times.py scripts help to better format the events and the execution time of each trace, but they are not necessary to execute in order to test the replayer.

To test the replayer, it is necessary to:

1) Install the requirements present in the requirements.txt file (needed also for the count.py and times.py scripts, present in requirements.txt);
2) Download Chrome Webdriver available at: https://chromedriver.chromium.org/home ;
3) Add the downloaded webdriver to PATH environmental variable;
4) Execute the PathsSimulator.py script.
