This page provides some development support in the form of howtos. 

# Drag and Drop

net.sf.jabref.external.DroppedFileHandler.handleDroppedfile(String, ExternalFileType, boolean, BibtexEntry) FileListEditor sets an TransferHandler inherited from FileListEditorTransferHandler. There, at importData, an DroppedFileHandler is instantiated and handleDroppedfile called. 

# Get the JabRef frame / panel

  * JabRef.jrf 
  * JabRef.jrf.basepanel() 

# Get Absolute/Expanded Filename

File f = Util.expandFilename(flEntry.getLink(), frame.basePanel().metaData().getFileDirectory(GUIGlobals.FILE_FIELD)); 

# Setting a Database Directory for a .bib File

  * @comment{jabref-meta: fileDirectory:&lt;directory&gt;} 
  * “fileDirectory” is determined by Globals.pref.get(“userFileDir”) (which defaults to “fileDirectory” 
  * There is also “fileDirectory-&lt;username&gt;”, which is determined by Globals.prefs.get(“userFileDirIndividual”) 
  * Used at DatabasePropertiesDialog 

# How to work with Preferences

Globals.prefs is a global variable storing a link to the preferences form. 

Globals.prefs.getTYPE(key) returns the value of the given configuration key. TYPE has to be replaced by Boolean, Double, Int, ByteArray. If a string is to be put, the method name is only “get”. 

To store the configuration keys in constants, one has two options 

  * as constant in the own class 
  * as constant in net.sf.jabref.JaRefPreferences.java 

There are JabRef classes existing, where the strings are hard-coded and where constants are not used. That way of configuration should be avoided. 

When adding a new preference, following steps have to be taken: 

  * add a constant for the configuration key 
  * in net.sf.jabref.JaRefPreferences.java put a “defaults.put(&lt;configuration key&gt;, &lt;value&gt;)” statement 

When accessing a preference value, the method Globals.prefs.getTYPE(key) has to be used. 

# Test Cases

If Globals.prefs are not initialized in a test case, try to add Globals.prefs = JabRefPreferences.getInstance(); 

# UI for Preferences

  * JabRefFrame.preferences() shows the preferences 
  * class: PrefsDialog3 

# "Special Fields"

## keywords sync

Database.addDatabaseChangeListener does not work as the DatabaseChangedEvent does not provide the field information. Therefore, we have to use BibtexEntry.addPropertyChangeListener(VetoableChangeListener listener) 