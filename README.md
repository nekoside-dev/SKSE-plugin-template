# SKSE-plugin-template

Support: Skyrim AE `1.7.104.0`

> I'm noob for Skyrim moddev, so it's not a perfect template.
>
> I create it for my using.

# Use

### Git

`git clone --recurse-submodules https://github.com/nekoside-dev/SKSE-plugin-template.git`

### Enviroment Variables

- Set `VCPKG_ROOT` to your vcpkg instance
- Set `SKYRIM_MODS_FOLDER` to your Mod Organizer 2 `mods` directory

### Visual Studio

Install C++ Desktop Development component. Ensure check the MSVC, cmake and vcpkg (or use cmake and vcpkg from scoop or CLion).

### Build

The plugin `dll` and `pdb` will be in `MO2\mods\<PROJECT_NAME>\`, replace the project name in `CMakeLists.txt`.
