### 1. Clone subject applications
The complete list of subjects (along with their GitHub URLs) used for the evaluation of *LeakPair* is available in the zipped folder of [Subjects](https://github.com/Arooba-git/leakpair-study-replication/blob/main/Subjects%20(LeakPair%20evaluation).zip). You may clone the subjects one by one and follow the subsequent steps.

### 2. Run the subject applications
#### Installation and Build
After cloning a subject, you may want to follow the instructions on its GitHub repository that specify the commands to install the necessary dependencies and to get the app up and running. In case of both a SPA library or website, the build script is usually `build`. Please execute the exact build script as specified in the respective `package.json` file (and GitHub instructions) to verify the code correctness before and after *LeakPair* execution (RQ 3).

#### Running a SPA website or webapp
*LeakPair* repairs applications built by SPA frameworks (React and Angular). Hence, if the project contains both server-side and client-side repositories, you may only want to start the client-side code to replicate the results (though starting the server in parallel will have no effect). After installing the subject dependencies, the script to get the web app running is generally `start`, so you may want to use the command `yarn start` or `npm run start`. Please verify the actual script from the `package.json file` or GitHub instructions.

#### Running a SPA library
SPA libraries are typically built and tested using [Storybook](https://storybook.js.org/), a framework that allows developers to test working demos of components and libraries on a localhost port. If your subject is a SPA library, the script to execute it would most likely be `storybook`. Hence, the command to get the demo running would be `yarn storybook` or `npm run storybook`. Please verify the actual script from the `package.json` file or GitHub instructions.

### 3. Run the test suite (if available)
In order to answer RQ3 (*Do the patches by LeakPair break the functionality?*), in addition to a successful program build/compilation, we also need to track the test suite results before and after *LeakPair* changes (if such test scripts are provided in `package.json`). Hence, as the subject is running, open another terminal and execute the test script. In most applications, this script is simply `test`, so you may want to run the command `yarn test` or `npm run test`. To view the actual script, as well as verify if a test script is provided at all, please check the `package.json` file. Some projects also have end-to-end testing scripts (e2e). All such scripts should be run, and their results noted, in order to assess *LeakPair*'s impact on the program's functionality later on.

### 4. Run Memlab
Once the subject is up and running, you can now install and run Memlab on your system, following their [official documentation](https://facebook.github.io/memlab/docs/installation). Please note that Memlab is a dynamic analysis tool; hence, it requires that the application under test be in a running state (either live or locally).

After ensuring Memlab's installation, you can run Memlab on the subject app by providing it with the absolute path to the scenario file:\
`memlab run --scenario [path-to-the-scenario-file] -v`

`-v` is optional but useful to see the details of the error in case Memlab terminates abruptly.


     IMPORTANT: You may want to confirm that the initial (localhost) URL provided in the scenario file is the same as the one
     opened up in your browser after starting the app; otherwise, Memlab will throw an error.

The complete list of scenario files for all the subject applications, is available in the zipped folder of [memlab-scenario-files](https://github.com/Arooba-git/leakpair-study-replication/blob/main/memlab-scenario-files.zip). Please select the respective scenario file by matching the name, for e.g, `roosterjs-scenario.js` for **roosterjs** project, `angular-components-scenario.js` for **angular-components** project, and so on. 

### 5. Take note of memory footprints
On the completion of its execution, Memlab logs the detailed statistics of the memory footprint of the app, including the count of leaking objects, retainer clusters, and the final heap size. An example below:

<img width="1051" alt="Screen Shot 2023-02-10 at 3 31 18 AM" src="https://user-images.githubusercontent.com/56495631/220322318-366fb07d-bcee-4a6b-8fa8-9fb9434a3247.png">

As you will discover in the documentation, Memlab also outputs the logs in a file format along with heap snapshots and some other meta data. However, for the evaluation of *LeakPair*, taking note of the count of leaking objects/clusters and the final heap size in the CLI would suffice.

### 6. Run LeakPair
After noting the initial memory footprints of the subject, you may now stop the application. You would now run LeakPair on the subject. You should already be able to run LeakPair if you have Node version 14 or above installed in your system (refer to the [README](https://github.com/Arooba-git/leakpair-study-replication) file for the command).

You can view the changes made by *LeakPair* using any diff tool if you want. An example of the Subscriptions leak fix in GitHub Desktop is shown below:
<img width="1178" alt="Screen Shot 2023-02-21 at 2 36 43 PM" src="https://user-images.githubusercontent.com/56495631/220335834-49359d08-2008-4c60-8872-07e2e09d0e66.png">

### 7. Re-run the subject applications (+ test suite)
Once *LeakPair* has made its changes, you need to restart the application by following the same commands as before.

#### RQ3: Do the patches by *LeakPair* break the functionality?
The subject should build and/or compile successfully after the changes. Also, if there were any test scripts available, run them again now (in another terminal, as done before). The count of passed/failing tests should remain unchanged.

### 8. Re-run Memlab
While the subject is still running, you can now run Memlab again with the same command and scenario file.

### 9. Take note of memory footprints (after *LeakPair* changes)
#### RQ1: How effective is *LeakPair*?
Take note of the count of leaking objects and the final heap size this time. As *LeakPair*  bases its efficacy on the reduction in the count of leaking objects or the heap size, at least one of them should show a noticeable reduction. You can compare your results with our evaluation results available in this [zipped folder of HTML files](https://github.com/Arooba-git/leakpair-study-replication/blob/main/Memory%20foot%20print%20evaluation%20results%20-%2025%20iterations.zip).

#### RQ2: Are the patches by *LeakPair* acceptable? 
As the review process is double-blinded, we plan to disclose the submitted PRs after the final decision to preserve anonymity, since the PRs were all created by the author's personal GitHub account (the status of the PRs at the time of submission, as well as the answer to this RQ are presented in Section 5.2 in the paper). 
