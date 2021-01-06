Bash script for the purpose of scanning your GOG offline installer collection for valid digital signatures and correct checksums, making sure your downloads have not been modified by someone else.
The script accepts multiple .exe files and folders as arguments. No arguments: check the current folder.

The script consist of 3 functions, run in this order:
1. sigcheck: checks .exe files for valid digital signatures
2. bincheck: checks if .bin files' checksums (which the .exe contains) are valid (only means something if sigcheck succeeds)
3. innocheck: test-extracts game files from both .exe and .bin files and verifies their checksums (sometimes which the .exe contains)

The script gogcheck tries to combine all 3 functions in one script.

Required packages (Debian/Ubuntu):
- sigcheck: osslsigncode
- bincheck: binutils
- innocheck: innoextract

For Windows users: The scripts also work with the Windows Subsystem for Linux (WSL) on Windows 10  
-> https://docs.microsoft.com/en-us/windows/wsl/

You may need to download or compile the latest version of innoextract if your distro's package is outdated.  
-> https://constexpr.org/innoextract/#download  
Some GOG games' .bin files are RAR archives. Their content's checksums are not known to the .exe file, so in such cases the innocheck script skips testing to save time.
As innoextract in general does take a long time to extract games, it is turned off by default unless you switch it on via command line option.

Q&A:
----

What does it mean if sigcheck's output goes green?

It means the string that went green is known to the script. The latter which contains a section in which you can put known-legit strings found in your purchased games. This pre-made string collection is not complete. However, as this optional feature is just there for visual convenience, to quickly spot both known and new strings, it does not affect osslsigncode's functionality.
