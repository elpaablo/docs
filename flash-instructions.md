## A/B updates

A few notes about the A/B update process, in case you're not familiar with it.

Aston uses a filesystem layout with 2 slots, slot a and slot b. Each slot will store the system in a certain state. When we flash/update the ROM, we are doing it from the active slot, where the system/recovery is running, and flashing to the other slot (inactive). After the update is finished, system will reboot and, if everything is ok, it will switch to the other slot, where the update was installed. Otherwise, it'll stay on the current slot and skip the update.

This is why we have to flash twice, if we wish to have the system in the same state in both slots.


# Flash instructions

## Clean install

You should use this method, when first installing the ROM or when switching between build types (GAPPS to MicroG or vice-versa). If you already have AlphaDroid recovery installed, you can reboot to recovery and start from step 3, otherwise start from step 1.

1 - Reboot to bootloader and flash AlphaDroid recovery to the active slot, using the provided [recovery.img](https://sourceforge.net/projects/alphadroid-project/files/aston/assets/recovery.img/download):

```fastboot flash recovery recovery.img>```

2 - Press volume down twice, until you see Recovery mode in the menu. Press the power button to reboot to recovery.

3 - Go to **Advanced**/**Enter fastboot** and wipe super partition, using the provided [super_empty.img](https://sourceforge.net/projects/alphadroid-project/files/aston/assets/super_empty.img/download):

```fastboot wipe-super super_empty.img```

4 - Press **Enter recovery** to go back to recovery mode. Press **Apply update** and then **Apply from ADB** to sideload the ROM to the inactive slot:

```adb sideload ROM.zip```

5 - Go back to recovery main menu, enter **Advanced** options and **Reboot to recovery**. This will send you to the newly installed recovery on the inactive slot (which will become active after rebooting).

6 - Sideload the ROM again, so that you have it installed in both slots.

7 - Go back to recovery main menu, press **Factory reset** and then **Format data/factory reset**.

8 - Go back to recovery main menu and reboot to system.

