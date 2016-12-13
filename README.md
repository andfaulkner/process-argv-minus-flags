# process-argv-minus-flags
Return process.argv with any flag arguments passed via the CLI excluded.

Flag arguments are defined as any parameters beginning with - or --, followed by 1 or non-dash (or space) character.
Also, any arguments containing an = that is both followed and preceded by one or more non-dash character is not considered a flag argument.

##(processArg?: Array<String>) => Array<String>
*   processArg: optional parameter containing a string array, presumably process.argv or a modified form of it. However, any array of strings can be used - it is not limited to process.argv
*   if no value is passed, defaults to the current value of process.argv
*   returns a duplicate of the array with all flag arguments removed.

###Examples

    //my-script.js
    const processArgvMinusFlags = require('process-argv-minus-flags');

    const contentArgsOnly = processArgvMinusFlags();
    console.log(contentArgsOnly);

Output values in example, based on how script was run from the terminal:
    //    input:  node my-script.js --verbose
    //          --> output --> ["node", "my-script.js"]
    //    input:  node my-script.js
    //          --> output --> ["node", "my-script.js"]
    //    input:  my-script.js --verbose create-component SidebarGrid
    //          --> output --> ["my-script.js", "create-component", "SidebarGrid"]
    //    myinput:  -script.js --verbose create-component SidebarGrid --debug
    //          --> output --> ["my-script.js", "create-component", "SidebarGrid"]
    //    input:  my-script.js --verbose create-component --name=SidebarGrid --debug
    //          --> output --> ["my-script.js", "create-component", "--name=SidebarGrid"]
    //          - the module doesn't exclude arguments containing an = sign


Other methods of calling processArgvMinusFlags function:

    const contentArgsOnly = processArgvMinusFlags(process.argv); // mainly for explicitness
    const contentArgsOnly = processArgvMinusFlags(['hello', '--flag', 'custom', 'array', 'example']); 


----

A trivial little utility, but one I found myself creating again and again across projects.
