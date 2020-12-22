# LANoireNX
LA Noire scripts used for repacking files from Switch version

- Python scripts are designed around Python 2, didn't test for Python 3. You need "numpy" for Python installed
- It is advised to not use cmd on Windows for python scripts. Use bash from WSL to unpack/pack correctly all big.nx files + unlock long paths in regedit/gpedit
- Textures are swizzled, format used for specified texture matches format used on PC, so you can copy DDS header from PC and replace them in .nxtex (0x78 bytes belong to header) or add them to .raw file at the beginning. Fonts are using BGRA8 format, rest textures either DXT5 (most cases) or DXT1
- Console versions of game are not using strings of root.atb to render text in main menu for "NEW", "RESUME", "EXTRAS", "CASES", "VEHICLE SHOWROOM" and "CREDITS". They are baked to props files you can find in props.big.nx/intermediate/chunks/props/game_menu/*language*/

bignx.unpack.py and bignx.pack.py were tested with:
- cases.big.nx + cases.big.nx.offsets.txt
- dlc.dlc1.big.nx + dlc.dlc1.big.nx.offsets.txt
- dlc.dlc2.big.nx + dlc.dlc2.big.nx.offsets.txt
- dlc.dlc3.big.nx + dlc.dlc3.big.nx.offsets.txt
- dlc.dlc4.big.nx + dlc.dlc4.big.nx.offsets.txt
- dlc.dlc5.big.nx + dlc.dlc5.big.nx.offsets.txt
- dlc.dlc6.big.nx + dlc.dlc6.big.nx.offsets.txt
- dlc.dlc7.big.nx + dlc.dlc7.big.nx.offsets.txt
- dlc.dlc8.big.nx + dlc.dlc8.big.nx.offsets.txt
- dlc.dlc9.big.nx + dlc.dlc9.big.nx.offsets.txt
- ui_streamed_textures.big.nx + ui_streamed_textures.big.nx.offsets.txt
- props.big.nx + props.big.nx.offsets.txt

Put those files and scripts in one folder. 
Edit **mainfile** string in python scripts to any ".big.nx" file. ".big.nx.offsets.txt" files are used to get filenames and paths for packing and unpacking files.
bignx.pack.py is packing ".big.nx" file to "output" folder. It takes file table from original ".big.nx" file, puts it to new file and patches it with correct sizes + offsets.
If in file table in ".big.nx" archive file has two sizes described, first data is pasted with original filename, second data is pasted with original filename + ".raw".

Because different big.nx files are using different page aligning, packing original files may result in different size. This is normal as I'm using page aligning "size & 0xF" because this is used by game for all big.nx files.

For extracting and patching wad + atb files I have modified 010 scripts from kramla's LANOIRE-TOOLS
# USAGE
> cases-atb-unpack.1sc (it works with DLC files too):
* Load this script to 010 editor
* Press F7
* Select .chunk.nx files in attribute folder for any unpacked .big.nx archive
* .chunk.nx.txt file will be generated in the same folder as .chunk.nx

If you want to extract different language change 0 from at lines 83 and 92 `k==0` to
* `0`- English
* `1` - French
* `2` - German
* `3` - Italian
* `4` - Japanese
* `5` - Russian
* `6` - Spanish

> cases-atb-pack.1sc (it works with DLC files too):
* Load this script to 010 editor
* Press F7
* Select chunx.nx.txt files in attribute folder for any unpacked .big.nx archive
* .chunk.nx file in the same folder will be patched with data from .chunk.nx.tx

If you want to replace different language change 0 from at lines 83 and 103 `k==0` to
* `0`- English
* `1` - French
* `2` - German
* `3` - Italian
* `4` - Japanese
* `5` - Russian
* `6` - Spanish

If 010 editor exits at some other language than English when importing data from txt files, try to open this txt file with Notepad++, convert EOL from Windows to Linux and go back to Windows from Linux, then save. If still exits, try to delete last 2 empty lines in Notepad++ and put one empty line by pressing enter at the end of file, then save.

> out-wad-unpack.1sc:
* Load out.wad.nx to 010 Editor
* Load out-wad-unpack.1sc to 010 editor
* Focus 010 Editor on out.wad.nx and press F7
* If list of scripts will be showed to choose, choose and run out-wad-unpack.1sc
* Files will be extracted to C:/LANOIRE/out

> out-wad-importer.1sc
* Put original out.wad.nx to C:/LANOIRE
* Load out-wad-unpack.1sc to 010 editor
* Press F7
* Files from C:/LANOIRE/out will be imported to out.wad.nx in C:/LANOIRE[/list]

> root-atb-unpack.1sc:
* Load this script to 010 editor
* Press F7
* Select root.atb.nx file that is in C:/LANOIRE/out/attribute
* root.atb.nx.txt file will be generated in the same folder as root.atb.nx[/list]

If you want to extract different language change 0 from at lines 83 and 92 `k==0` to
* `0`- English
* `1` - French
* `2` - German
* `3` - Italian
* `4` - Japanese
* `5` - Russian
* `6` - Spanish

> root-atb-pack.1sc:
* Load this script to 010 editor
* Press F7
* Select root.atb.nx.txt file that is in C:/LANOIRE/out/attribute
* root.atb.nx file that is in the same folder will be patched with data from root.atb.nx.txt[/list]

If you want to replace different language change 0 from at lines 83 and 103 `k==0` to
* `0`- English
* `1` - French
* `2` - German
* `3` - Italian
* `4` - Japanese
* `5` - Russian
* `6` - Spanish

BTW. thanks for 0 help from kramla because spending 15 minutes on explaining scripts seems too difficult for him.
