# Motion-RS

## Theory of Operation

Firmware is setup as a group of modules. Each module only needs a specific set of data from at least one other module to perform its task and pass data to the next module. 

### Modules
*
*

### [G-code parser](https://github.com/Michael-F-Bryan/gcode-rs)
|**State**|
|---------|
| None |
[G-code (RS-274)](https://en.wikipedia.org/wiki/G-code) is a simple language for defining tool motion on a CNC machine. The parser accepts a stream of characters from a source (either local or remote) and parses them into strongly typed objects.

```
pub struct Command {
    span: Span,
    line_number: Option<u32>,
    command_type: CommandType,
    command_number: u32,
    args: ArgBuffer,
}
```

### Position interpolation
|**State**|
|---------|
| SOM - System Of Measure (Metric or Imperial) |
| Tool position in the given SOM |
| Actual machine resolution in the given SOM (this is the smallest possible delta of motion) |
| Desired resolution in the given SOM |
| Relative or Absolute positioning |

For certain G-codes, the position interpolation module is executed to update an itermediate position buffer. This buffer provides absolute positions the tool should move to in the desired resolution in the selected SOM. It is possible to switch the SOM during tool operations. The output of this module goes into the Machine module.

### Machine module
|**State**|
|---------|
| TODO |

This module is dependent on the type of machine.  

### Stepper driver
|**State**|
|---------|
| TODO |

Provides a `trait StepperDriver` to enable custom tailored stepper drivers for each type of driver.
