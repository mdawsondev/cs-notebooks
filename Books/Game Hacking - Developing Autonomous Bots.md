# Game Hacking - Developing Autonomous Bots for Online Games

## Introduction

Just some general information on the history, ethics, and psycology of game hacking; nothing noteworthy.

## Part 1: Tools of the Trade

### Scanning Memory using Cheat Engine

Every toolkit used to hack games include the same four-piece setup: a *memory scanner*, an *assembly-level debugger*, a *process monitor*, and a *hex editor*. This chapter discusses [Cheat Engine](http://www.cheatengine.org) for memory scanning. [CrySearch](https://bitbucket.org/evolution536/crysearch-memory-scanner), although not mentioned, is a powerful open-source alternative.

Memory scanning is important because it allows programs to understand a game's "state". Although there are visually scriptable programs (AutoIt), memory scanners can pull variables and values directly from the process memory.

When a memory scanner is given a *scan value*, it loops through the memory array looking for the value equal to `x`. Every time it finds a matching value it adds the index to a result list. These scans tend to distribute large amounts of unwanted values due to sharing values in irrelevant data. To cast out the undesired variables the state of the game must have significant **entropy**, or a measure of disorder. Increasing entropy via moving, killing creatures, switching character, etc., disturbs addresses and shifts their values. This can let you filter undesireables.

### On Using Cheat Engine

Memmory scanners allow to different scan directives; *Scan Type* and *Value Types*. Scan Type tells the scanner how to compare the value with the memory being scanned, while value type tells the scanner what type of variable to search for.

* **Exact Value**: Returns address pointing to exact values; used for values you wont expect to change during the scan (health, mana, level, etc.).
* **Bigger Than**: Returns addresses pointing to values greater than the input; useful for something steadily increasing like timers.
* **Smaller Than**: Returns addresses pointing to smaller values, useful for something decreasing like countdowns.
* **Value Between**: Returns addresses between two values.
* **Unknown Initial Value**: Return all addresses allowing rescans to examine the entire range relative to their initial values. Useful for finding item or creature types.

Once the types have been set, running *First Scan* will populate the results list with initial values. *Green addresses* are static (remain persistant) and black values are in dynamically allocated memory (runtime). Results are displayed as real-time values, and rescans will show the value of each result during the previous scan. The real-time interval can generally be set to update as frequently as required.

Once the list is populated you can narrow your results by performing additional scans.

* **Increased Value**: Returns addresses pointing to values that have increased.
* **Increased Value By**: Returns addresses pointing to values increased by a defined amount.
* **Decreased Value**: Returns addresses pointing to values that have decreased.
* **Decreased Value By**: Returns addresses pointing to values decreased by a defined amount.
* **Changed Value**: Returns addresses pointing to values that have mutated.
* **Unhanged Value**: Returns addresses pointing to values that have not mutated.

Once values have been found, they can be added to the cheat table where they can be given a description, color, and can have their values displayed as hex or decimal. Data types and the values themselves can be changed here. These tables can be saved to a .ct document and imported for future use.

### Memory Modification in Games

Modifying the values of your memory will allow you to change them in-game, however, most online games have their stats store in a game server that is relayed to a local game client. Modifying values such as health, mana, skills, etc., are merely cosmetic and dont actaully change the values. Memory modification in an online game requires hacking far beyond Cheat Engine's capabilities. In local games with no remote server, all of these values can be changed at will.

The process of hooking to a value and changing it through CE is fairly simple.

1. Attach CE to game.
2. Scan for address or load table.
3. Double click value and open an input prompt.
4. Change the value.

If you want to ensure the value can't be overwritten, selecing the box under the Active colom will *freeze* the address.

### Trainer Generator

While manually changing values works great for quick hacks, constantly changing values is cumbersome and automated solutions are better. Trainers allow you to automate the whole memory modification without finding memory addresses.

Cheat Engine offers a trainer generator that will automate the memory modification process without the need to write any code. This is as easy as running `File > Create generic trainer Lua script from table`.

* **Processname**: The name of the executable the trainer hooks to.
* **Popup trainer on keypress**: Enables hotkey activation.
* **Title**: Title displayed in interface; optional.
* **About text**: Description displayed in interface; optional.
* **Freeze interval (in milliseconds)**: Interval during which a freeze operation overwites the value. This is typically best left at 250.

Once these values are set, clicking **Add Hotkey** will allow you to set up values from your cheat table. The hotkey cheats come with a variety of options.

* **Toggle freeze**: Toggles freeze state of the address.
* **Toggle freeze but allow increase**: Toggles the freeze state but allows the value to increase.
* **Toggle freeze but allow decrease**: Opposite of the above.
* **Freeze**: Sets to frozen if not already forzen.
* **Unfreeze**: Unfreezes if not frozen.
* **Set value to**: Sets value to specified value.
* **Decrease value with**: Decrease value by specification.
* **Increase value with**: Opposite of the above.

At this point, Cheat Engine runs the trainer in the background and you can use your hotkeys. To save the trainer to a portable executable, clicking *Generate trainer* will output the file. Running this executable will hook the trainer to the game without needing to start CE.

### Pointer Scanning

While dynamic memory addresses are useless on their own, some static addresses will point to another address, pointing to another address, and so on, until the tail of the cain points to the address we're interested in. CE can find these chains using *point scanning*.

#### Pointer Chains

Pointer chains look like linked lists `list<int> chain = {start, offset1, offset2[, ...]}`. The first value in the chain is called a *memory pointer*, and the remaining values are called a *pointer path*.

``` c++
int readPointerChain(chain) {
  ret = read(chain[0])
  for i = 1, chain.len - 1, 1 {
    offset = chain[i]
    ret = read(ret + offset)
  }
  return ret
}
```

Represented in pseudocode, this function takes a pointer chain called `chain` as a parameter and then treats the path as a list of memory offsets from the address `ret`. It loops through each offset, updating the value of `ret` on each iteration and returning `ret` once it's finished. Not mentioned in the book, but this sounds like how linked lists function when trying to navigate to the final node.

_Aside: Many game hackers prefer to have their chains in place rather than encapsulating them in functions._

From a reverse engineering perspective, you could analyze the assembly code and find what pointer path accessed which value, but that takes a lot of time and advanced tools. **Pointer scaners** solve this by brute-forcing to recursively iterate over every possible chain until they find one that leads to the target address.

``` c+++
list<int> pointerScan(target, maxAdd, maxDepth) {
  for address = BASE, 0x7FFFFFF, 4 {
    ret = rScan(address, target, maxAdd, maxDepth, 1)
    if (ret.len > 0) {
      ret.pushFront(address)
      return ret
    }
  }
  return {}
}

list<int> rScan(address, target,maxAdd, maxDepth, curDepth) {
  for offset = 0, maxAdd, 4 {
    value = read(address + offset)
    if (value == target)
      return list<int>(offset)
  }
  if (curDepth < maxDepth) {
    curDepth++
    for offset = 0, maxAdd, 4 {
      ret = rScan(address + offset, target, maxAdd, maxDepth, curDepth)
      if (ret.len > 0) {
        ret.pushFront(offSet)
        return ret
      })
    }
  }
  return {}
}
```

The psuedocode above shows how a pointer scanner works internally. `pointerScan()` is the entry point. It takes parameters to loop through every 4-byte alined address in the game, calling `rScan()`. `rScan()` reads memory from every 4-byte alined offset between 0 and maxAdd and returns a result if it's equal to target. Otherwise, it loops over and increments through each offset.

Although the method above shows basic functionality, it's insanely slow and would generate a lot of false positives. There are better alternatives for navigating a pointer chain.

#### Pointer Scanning with Cheat Engine

To scan in Cheat Engine, right-click on a dynamic memory address in the table and select `Pointer scan for this address`, where you will then be asked where to store can results as a _.ptr_ file. Once chosen, this will open a Pointerscanner scanoptions dialog window with several options.

Key Options:

* **Addresses must be 32-bits aligned**: Only scan addresses that are multiples of 4; compilers align data so that most addresses are multiples of 4 by default. This option will rarely need to be disabled.
* **Only find paths with a static address**: Prevents searching paths with a dynamic starter point. This option should always be enabled because scanning for a path starting at another dynamic address is counterproductive.
* **Don't include pointers with read-only nodes**: Should always be enabled; dynamically allocated memory storing volitile data should never be read-only.
* **Stop traversing a path when a static has been found**: Exits the scan when a pointer path with a static start address is found; should be enabled to reduce false positives.
* **Pointer path may only be inside this region**: Can typically be left as is; other options compensate for the large range by narrowing the scope.
* **First element of pointerstruct must point to module**: Instructs CE not to search heap chunks with virual function tables under the assumnption that the game was coded using OOP. This is highly unreliable and should almost always be left disabled.
* **No looping pointers**: Invalidates any path that points to itself which discards inefficient paths.
* **Max level**: Determines max length of the pointer path; kept around 6 or 7 nodes.

Situational Options:

* **Improve pinterscan with gathered heap data**: Uses heap allocation record to determine offset limits; typically left enabled for the first scan but should be the first to go if you're unable to find reliable paths.
* **Only allow static and heap addresses in the path**: Invalidates paths that can't be optimized with heap data.
* **Max different offsets per node**: Limits the number of same-value pointers that are checked; i.e. only checking pointers once. This is useful to narrow down result sets, but may miss many valid paths.
* **Allow stack addresses of the first thread(s) to be handled as static**: Scans call stacks of oldest `m` threads in game, checking the first `n` bytes in each. Paths found with this option are highly volitile and useful; used when failed to find heap addresses
* **Stack addresses as only static addresses**: Take previous option further by allowing only stack addresses in pointer paths.
* **Pointers must end with specific offsets**: Useful if offsets at the end of a path are known.
* **Nr of threads scanning**: Number of threads the scanner will use; a number rqual to the number of your cores will often work best. Idle is slow, Normal is used for most scans, nad Time critical is for large scans.
* **Maximum offset value**: Determine max value of each offset in path. Typically start low and increase if the scan fails; 128 is a good starting value.

Using the rescan feature will help eliminate false positives. Ctrl-R from the results window will open the rescan pointerlist dialog window where two main options should be considered.

* **Only filter out invalid pointers**: If checked, the rescan will discard only pointer chanins that point to invalid memory which helps if the initial result set is large. Disable to filter paths that don't resolve to specific addressss.
* **Repeat rescan until stopped*: If checked, will rescan in a continuous loop. Should be enabled while creating a large amount of entropy.

For inital rescans, enabling both of these options is a good idea. The rescan window will vanish and a `Stop` button will appear in the window. You should create a few minutes of entropy before stopping the scan. In some cases rescanning will still leave you with a large list of options. When this happened, the game may need to be restarted to find the address that holds your value then rescan on this specific address to further narrow results. In this scan, leave invalid pointers **unchecked** and enter the new address in the **address to find** field.

If the results *still* aren't narrow enough, try running the scan across system restarts or even different systems. If this is still a large result, they should be considered static because more than one pointer chain can resolve to the same address.

Once narrowed down, double-click on a useable pointer chain to add it to the cheat table. If you have multiple results, grab the one with the fewest offsets. If multiple chains have identical offsets, the data is possibly stored in a dynamic data structure.

_p18_