# 🎣 mc-fish-pye

AFK auto-fishing script for Minecraft using Python and OpenCV.

So that you can bake many [fish p*y*es](https://en.wikipedia.org/wiki/Fish_pie) with all the fish you get :)

## ⚙️ Setup

To use this script, you will need to:
- Install Python and the following packages (you can use [venv](https://docs.python.org/3/library/venv.html)):
  - For `main.py`: [OpenCV](https://pypi.org/project/opencv-python/), [PyAutoGUI](https://pypi.org/project/PyAutoGUI/) and [keyboard](https://pypi.org/project/keyboard/)
  - For `setup.py`: [pynput](https://pypi.org/project/pynput/)
- Run `setup.py` and perform two clicks to define the region of interest
- Update `config.json` to use the newly defined ROI:
```json
{
    "startTimer": 5,
    "detection": {
        "roi": {
            "x1": 1000,
            "x2": 2000,
            "y1": 1000,
            "y2": 2000
        },
        "threshold": 10,
        "cooldown": 2.5
    },
    "actions": {
        "clickPos": {
            "x": 0,
            "y": 0
        },
        "clickDelay": 0.5
    }
}
```
- Download the [resource pack](./resource-pack/) and import it (Feel free to zip it if you want)
- In game, select the resource pack and then change your in-game language to "Bionic Fisher Lang"
- Make sure you have the [subtitles](https://minecraft.wiki/w/Subtitles) enabled in **Accessibility Settings**
- In **Accessibility Settings**, disable the transparency of the subtitle background (it should be full black)
- Make sure you do not have **Friendly Creatures** sounds muted in your **Sound Settings**

## 📖 Usage

- Launch Minecraft and make sure you have set your language properly
- Join a world and stand in front of your fishing spot
- Run the `main.py` script with root/admin privileges (required for the keyboard key press)
- Quickly switch window focus to Minecraft and let it do the work
- Enjoy an infinite supply of fish and treasure!
- You can stop the script at any moment by holding the `p` key 

## ❓ How it works

This script relies on Minecraft subtitles and a custom language to detect when the fishing bobber sinks.

The custom language sets all subtitles to be empty, apart from `subtitles.entity.fishing_bobber.splash`, which is set to "AAAAAAA".

The long string will cause the black background behind the subtitle text to stretch farther than other subtitles.

These additional black pixels are what the script is looking for to detect if your fishing bobber has caught onto something.

Once a catch is detected, the script sends one right click to retrieve the catch, followed immediately by another one to cast the rod again.

After the rod has been cast again, the pixel detection will be deactivated for a few seconds to allow the subtitle to have time to fade away.
