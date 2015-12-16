# xboxdrv.config

Repository of [xboxdrv](https://github.com/xboxdrv/xboxdrv) config files for non-standard controllers and adapters.

Plug in your controller and look for MY_DEVICE in

    ls -l /dev/input/by-id/

Then start xboxdrv with the matching device.

    xboxdrv -c $MY_DEVICE.xboxdrv

## New config

If your controller doesn't have a config, you can create one in just a few minutes.
First, map out your controller by pushing buttons while running

    evtest /dev/input/$MY_DEVICE

Now create `$MY_DEVICE.xboxdrv`, following this template:

    [xboxdrv]
    evdev      = /dev/input/by-id/$MY_DEVICE
    evdev-grab = true
    mimic-xpad = true
    deadzone   = 3000

    [axis-sensitivity]
    X1 = -0.7
    X2 = -0.7
    Y1 = -0.7
    Y2 = -0.7

    # Raw controller inputs on the left map to the xbox equivalent on the right.

    [axismap]
    -Y1 = Y1
    -Y2 = Y2

    [evdev-absmap]
    ABS_X  = X1
    ABS_Y  = Y1
    ABS_Z  = X2
    ABS_RZ = Y2
    ABS_HAT0X = DPAD_X
    ABS_HAT0Y = DPAD_Y

    [evdev-keymap]
    BTN_B = A
    BTN_C = B
    BTN_A = X
    BTN_X = Y
    BTN_Y = LB
    BTN_Z = RB
    BTN_TL = LT
    BTN_TR = RT
    BTN_SELECT = TL
    BTN_START = TR
    BTN_TL2 = BACK
    BTN_TR2 = START
    BTN_MODE = GUIDE

Now run xboxdrv and read the output to verify that the mapping is correct.

    xboxdrv -c $MY_DEVICE.xboxdrv

Once done, please submit a pull request to share your config or to suggest an improvement.

## License

By submitting code to this repository, you agree to distribute it under a [GPL-compatible license](https://www.gnu.org/licenses/license-list.html#GPLCompatibleLicenses).
All files shall be GPLv3 licensed, unless specified otherwise.

## Project Roadmap

- More configs!
- Automatic loading (exec from udev rule?).
- Hide base js0 for games that expect one controller.
