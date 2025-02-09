# P2-FLASH-FS / REF
Versioned releases from Chip which we roll into the formal verison.

![Project Maintenance][maintenance-shield]

[![License][license-shield]](LICENSE)


## Versions from Chip
This is a recap of the version history of files arriving from Chip:

| Version | Date | Purpose |
| --- | --- | --- |
|  v1.0 | <PRE>2023-08-14</PRE> | Initial release.	 |
| v1.1 |  <PRE>2023-08-18</PRE> | Optimized SPI to 8 clocks/bit, or 40MHz SPI_CK at 320MHz. SPI\_CS now resets high.	|
| v1.2 |  <PRE>2023-08-25</PRE> | Adds open_append(), cleans up byte counting, adjusts get new handle to set filename for handle.

## The latest Files from Chip

This is the latest files from the [Forum Thread](https://forums.parallax.com/discussion/175470/on-board-flash-file-system/p2)

| File | Purpose |
| --- | --- |
| [FlashFileSystem_16MB.spin2](FlashFileSystem_16MB.spin2) | Chip's latest found in the forums |
| [FlashFileSystem_16MB_Demo.spin2](FlashFileSystem_16MB_Demo.spin2) | A demo using Chip's driver |

## Files for Review by Stephen

This is my work in progress as I'm working toward customer facing release of the FileSystem code. This step happens just before final integration with the live flash driver.

| File | Purpose |
| --- | --- |
| [Draft\_FlashFileSystem_16MB_Demo.spin2](Draft_FlashFileSystem_16MB_Demo.spin2) | A Demo of the filesystem code reworked for publication |
| [Draft\_FlashFilesystem_16MB.spin2](Draft_FlashFilesystem_16MB.spin2) | A draft of the filesystem code reworked for publication |
| [Draft\_FlashFilesystem_16MB.txt](Draft_FlashFilesystem_16MB.txt) | The Object Interface document generated from the new draft |


### Next Steps:

- Keep up with Chip's changes:
  - Integrate read/write/modify version from Chip when it arrives
- ... more I'm sure ...

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
