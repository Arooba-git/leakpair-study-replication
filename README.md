# LeakPair
Proactive repairing of memory leaks in Single Page Applications

## Installation and Usage

1. Since *LeakPair* is an npx command tool, the only requirement for running it is to ensure you have Node installed in your system. LeakPair support node versions >= 14.
 
     - #### On Windows and Mac
        Visit the official [Node](https://nodejs.org/en/download/) website and follow the instructions for your OS. This will install the latest version of Node on your system. This will also install the Node Package Manager (npm) and the node packages executor (npx) on your system. Check their successful installation with `node -v`, `npm -v`, and `npx -v` respectively.
 
    - #### On Linux based systems
      Use the command `sudo apt install npm`. This will automatically install node, npm , and npx. However, the installed node version will be `v12.22.9`, while LeakPair require at least version 14. For that, install a node version manager globally on your system: `npm install -g n`. 

      Now you can use `n 14.0.0` to install the supported version. Note that you can replace this version with any version higher than 14,  including `n latest`.&nbsp;

2. Once the supported version of node is installed, you can install LeakPair globally on your system with the command `npm install leakpair -g`.

3. You can now run LeakPair with the command `npx leakpair [path]` where `path` is the **absolute** path of the repository or file that you wish to repair for memory leaks. Note that LeakPair only supports `.js`, `.jsx`, `.ts` and `.tsx` files. That is, if you provide the path to a repository, it will only filter and process files with these extensions.

4. By default, LeakPair will log the memory leak and repair statistics directly in the CLI. However, if you wish to store it in a file format, you can provide an optional argument for the output path: `npx leakpair [path-of-project-to-repair] [path-for-output]`

**Example** `npx leakpair /Users/arooba/roosterjs  /Users/arooba/Desktop`
<br />
In this case, an `output.txt` file will be generated containing the leaks and repair statistics of roosterjs, in the user's Desktop directory.

#### Example of *LeakPair*'s output log in CLI
<img width="558" alt="Screen Shot 2023-02-21 at 2 42 25 PM" src="https://user-images.githubusercontent.com/56495631/220257699-400404de-0402-4375-9f6d-29e68d9975ad.png">
