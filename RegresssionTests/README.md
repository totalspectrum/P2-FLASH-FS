# P2-FLASH-FS / Regresssion Tests

![Project Maintenance][maintenance-shield]

[![License][license-shield]](LICENSE)

These are regression test files that I'm using to certify the FS operation with each release.  All tests must pass! The regression test programs are versioned here so you can repeat this testing any time to verify your driver operation.

The point of these tests is to exercise each method attempting to check both normal and error/exception cases.

## Test Coverage

The Regression test coverage is nearly complete!  This table indicates which methods have been test by the current regression test programs.

| Public Method | tested | Notes
| --- | --- | --- |
| PUB version() : result | YES
| PUB serial_number() : sn\_hi, sn\_lo | YES
| PUB mount() : status | YES
| PUB unmount() | YES
| PUB format() : status | YES
| PUB error() : result | YES
| PUB open(p_filename,"r") : handle | YES
| PUB open(p_filename,"w") : handle | YES
| PUB open(p_filename,"a") : handle | YES
| PUB open(p_filename,"r+") : handle | | Not in initial release
| PUB open\_circular(p_filename,"r") : handle | YES
| PUB open\_circular(p_filename,"a") : handle | YES
| PUB flush(handle) : status | YES
| PUB close(handle) : status | YES
| PUB rename(p_old_filename, p_new_filename) : status | YES
| PUB delete(p_filename) : status | YES
| PUB exists(p_filename) : result | YES
| PUB file\_size(p_filename) : size\_in\_bytes | YES
| PUB file\_size\_unused(p_filename) : size\_in\_bytes\_unused | YES
| PUB seek(handle, position) : result | YES
| PUB write(handle, p_buffer, count) : result | YES
| PUB wr_byte(handle, byteValue) : result | YES
| PUB wr\_word(handle, word_value) : result | YES
| PUB wr\_long(handle, long_value) : result | YES
| PUB wr\_str(handle, p_str) : result | YES
| PUB read(handle, p_buffer, count) : bytes\_read | YES
| PUB rd_byte(handle) : value | YES
| PUB rd_word(handle) : value | YES
| PUB rd_long(handle) : value | YES
| PUB rd\_str(handle, p_str, count) : result | YES
| PUB directory(p\_block\_id, p\_filename, p\_file\_size) | YES
| PUB stats() : used\_blocks, free\_blocks, file\_count | YES
| PUB string\_for\_error(error_code) : p\_interpretation | YES


## Running the tests

In order the compile the tests you need to uncomment the test-support routines in `Draft_flash_fs.spin2`. Look for line 1705:

#### Driver file: Draft\_flash\_fs.spin2: line 1705
```spin2
{   ' REMOVE BEFORE FLIGHT: uncomment this line before release!!!

' ----------------------------------------------------------------------------------------------
'   these methods are for regression testing only - they are not used in production code
```
comment out the 1st line to enable the code that follows. [ place a ' before the {... ]


#### Determine debug output routing (RT_*.spin2 files)

At the head of each of test RT .spin2 files you want to run look for the debug output lines:

```spin2
{
    ' debug via serial to RPi (using RPi gateway pins)
    DEBUG_PIN_TX = 57
    DEBUG_PIN_RX = 56
    DEBUG_BAUD = 2_000_000
'}
```

These lines when uncommented route the debug serial to PINs 56/57 which I connect to the a Raspberry Pi for logging as there is lot of output from the test runs.

In their present for (commented out) the debug output just goes the debug window on windows where you are running the compiler.


## The Test files 

This is a recap of the version history of these files:

| Date | Status |
| --- | --- |
|  <PRE>2023-Aug-26</PRE> | Initial release. `RT_read_write_tests.spin2`<br>Working Format, Mount, open(file, "R"), open(file, "W"), close(),<br>Focused tests for wr\_byte(), rd\_byte(), wr\_word(), rd\_word(), wr\_long(), rd\_long(), wr\_str(), and rd\_str() <br>Spanning blocks tests need to be added|
|  <PRE>2023-Aug-27</PRE> | More Tests: `RT_read_write_block_tests.spin2`<br>Working Format, Mount, open(file, "R"), open(file, "W"), close(),<br>Focused tests for read(), write(), and file\_size_unused(): in only block, spanning two blocks, spanning 3 blocks |
|  <PRE>2023-Aug-28</PRE> | More Tests: `RT_read_seek_tests.spin2`<br>Working Format, Mount, open(file, "R"), open(file, "W"), close(),<br>Focused tests for seek(): in only block, spanning two blocks, spanning 3 blocks |
|  <PRE>2023-Aug-29</PRE> | **Updated** `RT_read_write_tests.spin2`<br>Working Format, Mount, open(file, "R"), open(file, "W"), close(),<br>Focused tests for wr\_byte(), rd\_byte(), wr\_word(), rd\_word(), wr\_long(), rd\_long(), wr\_str(), and rd\_str() <br>Added tests for version(), serial_number(), directory(), and 2, 3 block span tests using longs |
|  <PRE>2023-Sep-02</PRE> | More Tests `RT_write_append_tests.spin2`<br>Working Format, Mount, close(),<br>Focused tests for open(file, "A"), wr\_byte(), rd\_byte(), wr\_word(), rd\_word(), wr\_long(), rd\_long(), wr\_str(), and rd\_str() with additional tests for 2, 3 block span tests using longs |
|  <PRE>2023-Sep-08</PRE> | More Tests `RT_mount_handle_basics_tests.spin2`<br>This tests all methods when filesystem is not mounted, when we are out of handles and when attempting to use an illegal handle<br>The point of this testing is to ensure that methods are returning the proper error code as documented under these conditions 
|  <PRE>2023-Sep-08</PRE> | More Tests `RT_read_write_circular_tests.spin2`<br>This is the full test suite exercising the open_circular() for read and append methods. They ensure that blocks are added to and removed from the filesystem as they should be. They also ensure the reading from the circular file starts at the byte that they should be. These tests use 1KB records when id and checksum in each so that the reads can be certified to start at the exact byte they should be.
|  <PRE>2023-Sep-12</PRE> | More Tests `RT_read_write_append_tests.spin2`<br>Added testing of flush() method when used with appends.
|  <PRE>2023-Sep-12</PRE> | More Tests `RT_read_write_tests.spin2`<br>Added testing of unmount() and mount() methods
|  <PRE>2023-Sep-13</PRE> | More Tests `RT_read_seek_tests.spin2`<br>Added testing of seek()'s new "current position relative" feature
|  <PRE>2023-Sep-19</PRE> | More Tests `RT_read_write_8cog_tests.spin2`<br>Added testing of multi-cog support

## Test files by Stephen

This is my work in progress as I'm working toward customer facing release of the FileSystem code


| File | Purpose |
| --- | --- |
| [RT\_utilities.spin2](RT_utilities.spin2) | Utility methods common to all Test Files |
| [RT\_mount\_handle\_basics_tests.spin2](RT_mount_handle_basics_tests.spin2) | The read/write basic types test suite |
| [RT\_mount\_handle\_basics_tests.log](RT_mount_handle_basics_tests.log) | Log of the read/write basic types tests [85 passes, 0 fails] |
| [RT\_read\_seek_tests.spin2](RT_read_seek_tests.spin2) | The open for read seek test suite |
| [RT\_read\_seek_tests.log](RT_read_seek_tests.log) | Log of the open for read seek tests [97 passes, 0 fails] |
| [RT\_read\_write\_8cog_tests.spin2](RT_read_write_8cog_tests.spin2) | The multi-cog testing suite |
| [RT\_read\_write\_8cog_tests.log](RT_read_write_8cog_tests.log) | Log of the multi-cog tests [231 passes, 0 fails] |
| [RT\_read\_write\_8cog\_tests_byCog.log](RT_read_write_8cog_tests_byCog.log) | Log of the multi-cog tests - **Sorted by COG** [231 passes, 0 fails] |
| [RT\_read\_write\_block_tests.spin2](RT_read_write_block_tests.spin2) | The read/write records(blocks) test suite  |
| [RT\_read\_write\_block_tests.log](RT_read_write_block_tests.log) | Log of the read/write records(blocks) tests  [42 passes, 0 fails] |
| [RT\_read\_write\_circular_tests.spin2](RT_read_write_circular_tests.spin2) | The read/write circular test suite |
| [RT\_read\_write\_circular_tests.log](RT_read_write_circular_tests.log) | Log of the read/write circular tests [247 passes, 0 fails] |
| [RT\_read\_write_tests.spin2](RT_read_write_tests.spin2) | The read/write basic types test suite |
| [RT\_read\_write_tests.log](RT_read_write_tests.log) | Log of the read/write basic types tests [102 passes, 0 fails] |
| [RT\_write\_append_tests.spin2](RT_write_append_tests.spin2) | The open for append test suite |
| [RT\_write\_append_tests.log](RT_write_append_tests.log) | Log of the open for append tests [102 passes, 0 fails] |

### Next Steps:

- certify life-cycle changes for blocks of files created/modified (this is visuall checked for now...)
- finish tests for read-modify write modes (*When this feature arrives, soonish*)
- ...

---

> If you like my work and/or this has helped you in some way then feel free to help me out for a couple of :coffee:'s or :pizza: slices!
>
> [![coffee](https://www.buymeacoffee.com/assets/img/custom_images/black_img.png)](https://www.buymeacoffee.com/ironsheep) &nbsp;&nbsp; -OR- &nbsp;&nbsp; [![Patreon](../DOCs/images/patreon.png)](https://www.patreon.com/IronSheep?fan_landing=true)[Patreon.com/IronSheep](https://www.patreon.com/IronSheep?fan_landing=true)

---

## Disclaimer and Legal

> *Parallax, Propeller Spin, and the Parallax and Propeller Hat logos* are trademarks of Parallax Inc., dba Parallax Semiconductor
>
> This project is a community project not for commercial use.
>
> This project is in no way affiliated with, authorized, maintained, sponsored or endorsed by *Parallax Inc., dba Parallax Semiconductor* or any of its affiliates or subsidiaries.

---

## License

Licensed under the MIT License. Copyright © 2023 Iron Sheep Productions, LLC.

Follow these links for more information:

### [Copyright](copyright) | [License](LICENSE)

[maintenance-shield]: https://img.shields.io/badge/maintainer-stephen%40ironsheep%2ebiz-blue.svg?style=for-the-badge

[license-shield]: https://camo.githubusercontent.com/bc04f96d911ea5f6e3b00e44fc0731ea74c8e1e9/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f69616e74726963682f746578742d646976696465722d726f772e7376673f7374796c653d666f722d7468652d6261646765

