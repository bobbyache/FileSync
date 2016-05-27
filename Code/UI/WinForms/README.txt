
Comparing Files for Changes:
http://stackoverflow.com/questions/1358510/how-to-compare-2-files-fast-using-net

Known Bugs
----------------------------------------------------------------------------------------------------------------

CONSIDER RATHER THAN POPPING UP A DIALOG EVERY TIME A FILE IS MISSING OR ALREADY EXISTS, SIMPLY COMPILE A REPORT
TO SHOW THESE ITEMS ONCE THE COPY HAS BEEN COMPLETED!!! IT'S FUCKING IRRITATING.
Actually very simple to do, just modify listView1_DragDrop and create a dialog window to send the information
there...
----------

* Add option to remove missing target files from your project.

----------------------------------------------------------------------------------------------------------------
		* It would be better to have an event raised that will change the listview contents after modifying
		the contents... currently you're doing this manually. Better to have a "SyncItems_Changed" event that
		can just be raised?

        public void RemoveMissingTargetFilesFromList()
        {
            SyncItem[] items = GetMissingTargetFileItems();
            foreach (SyncItem item in items)
            {
                syncItems.Remove(item);
            }
        }

        public static DialogResult PromptRemoveMissingTargetFiles(IWin32Window owner)
        {
            return MessageBox.Show(owner, "Sure you want to remove all missing target files from your project?", "Remove",
                MessageBoxButtons.YesNoCancel, MessageBoxIcon.Information, MessageBoxDefaultButton.Button2);
        }
----------------------------------------------------------------------------------------------------------------


* When backing up the target and working folder, you should backup the corresponding project file as well so that
you can completely re-establish the state the project was in before hand!


* Currently, if your target file has the same name as another target file you can get around this problem by
saving the file into a different working sub-directory with the same name, or just rename the working file
so that the conflict doesn't occur. However, when the auto-backup creates another directory it puts all files
inside that directory. Some of the files will be inappropriately over-written if they have the same name.

Future solutions:
1. Don't allow duplicate names for working files, regardless of whether they are in the same directory or not.
	or
2. Try to rename the backup files, but this might add some complexity.
3. Add duplicate files to a different sub-folder, but this might increase complexity.