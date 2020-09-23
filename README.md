<div align="center">

## Universal File Handler


</div>

### Description

There is a lot you can do with this class! See the code to see the exact methods and how they work. You can delete files, copy files, insert a line into a file (alphabetically or append at end), search for a line, retrieve the nth line as a String, count the number of lines in the files, and more!
 
### More Info
 
Simply paste the code below into a file, UniversalFileHandler.java... you have to configure two variables to make sure the files will to go to the directory you want them to go to. To use the code, create a new instance in another class... like UniversalFileHandler uFileHandler = new UniversalFileHandler();


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Jennica Jane Humphrey](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/jennica-jane-humphrey.md)
**Level**          |Intermediate
**User Rating**    |4.7 (33 globes from 7 users)
**Compatibility**  |Java \(JDK 1\.2\)
**Category**       |[Files/ File Controls/ Input/ Output](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files-file-controls-input-output__2-58.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/jennica-jane-humphrey-universal-file-handler__2-2417/archive/master.zip)





### Source Code

```
import java.io.*;
class UniversalFileHandler {
/**********************************************************
 *
 * UNIVERSAL FILE HANDLER
 * UniversalFileHandler.java
 *
 * The goal here is to be as encapsulated as possible.
 * This class should be reuseable for a wide variety of
 * purposes and have no "specialization" whatsoever
 * for my particular applications.
 *
 * Does various things with files. Like, delete,
 * create, insert a line into a file in lexiconial
 * order and all that.
 *
 *********************************************************
 *
 * CUSTOMIZING IT FOR YOUR USE
 *
 * All you need to do is modify the filePath and
 * the fileSlash variables at the end of the class.
 *
 * FILEPATH: The directory you want to place the
 * files in.
 *
 * FILESLASH: Windows users should
 * keep the fileSlash variable unchanged at "\\".
 * Linux probably should change the variable to
 * "/".
 *
 *********************************************************
 *
 * METHODS INCLUDED IN THIS CLASS
 *
 * There is a lot you can do with this class! Here are
 * the methods, as they appear in this class (see the
 * actual methods themselves to find out how to use them):
 *
 * deleteFile: Deletes a file.
 *
 * createFile: Creates a (blank) file.
 *
 * fileExists: Checks to see if a file exists.
 *
 * copyFile: Copies the original file into a new file.
 *
 * searchForString: Searches for a partial string in the
 * file at the beginning of a new line.
 *
 * numberOfLines: Returns the number of lines in a given
 * file.
 *
 * returnFullString: Returns the full line of a partial
 * string at the beginning of a line (ie, if you search for
 * "ABC", you'll get "ABCDEFGHIJKLMNOPQRSTUVWXYZ" returned)
 *
 * retrieveEndLineChar: Returns the last character in a
 * specified line in the file.
 *
 * writeIntoFile: Writes a line at the end of the file.
 *
 * insertIntoFile: Inserts a line in the file in
 * alphabetical order.
 *
 * deleteFromFile: Deletes a single line from the file.
 *
 * getLine: Returns the nth line from the file.
 *
 ***********************************************************
 *
 * If you see any errors in this code, please contact
 * me at emelia2002@hotmail.com. Please keep the comments
 * on this java file unchanged and keep my name and email.
 *
 * I created this class for a school project and it just
 * kept growing and growing... I hope people will get as
 * much use out of this as I have.
 *
 * Feel free to use this class in whatever way you want.
 * I've used it with almost all of my applications that
 * relate to file manipulation... it has been a great
 * timesaver. My java knowledge is largely self-taught,
 * so please pardon any gaffes I make.
 *
 * @see  RandomAccessFile
 * @see  File
 * @author Jennica Humphrey (emelia2002@hotmail.com)
 * @version %I%, %G%
 * @since JDK1.3
 *
 */
 /**
 * Deletes the file if it does already exist.
 *
 * @param fileName Name of the file to be deleted.
 * @see  File
 * @since  JDK1.3
 */
 public void deleteFile(String fileName) {
  String path = new String();
  path = filePath; // uses the filePath directory
  File f1 = new File( path, fileName);
  if (f1.exists())
  f1.delete();
 } // Ends deleteFile
 /**
 * Creates the file if it does already exist.
 *
 * @param fileName Name of the file to be deleted.
 * @return  TRUE if file is successfully created,
 *    FALSE if it already exists or if some
 *   other error happens.
 * @see  File
 * @since  JDK1.3
 */
 public boolean createFile(String fileName) {
  String path = new String();
  path = filePath; // uses the filePath directory
  boolean fileCreated = false;
  File f1 = new File( path, fileName);
  if ( !f1.exists() ) {
  try {
   f1.createNewFile();
   fileCreated = true;
  }
  catch( IOException e ) {
  }
  }
  return fileCreated;
 } // Ends createFile
 /**
 * Checks to see if a file exists.
 *
 * @param fileName Name of the file to be deleted.
 * @return  TRUE if the file exists, FALSE if the file
 *    does not exist.
 * @see  File
 * @since  JDK1.3
 */
 public boolean fileExists(String fileName) {
 // Makes sure file exists
  String path = new String();
  path = filePath; // Uses the filePath dir
  boolean fileFound = false;
  File f1 = new File(path, fileName);
  if (f1.exists())
  fileFound = true;
  return fileFound;
 } // ends fileExists
 /**
 * Copies a file (assuming it exists) into a new file.
 *
 * @param fileName  Name of the file to be copied.
 * @param copiedFileName Name of the file to be written into.
 * @see   RandomAccessFile
 * @see    #fileExists
 * @see    #createFile
 * @since    JDK1.3
 */
 public void copyFile(String fileName, String copiedFileName) {
 // Copies one file into a new file (if that file doesn't exist )
  if ( fileExists(fileName) ) // Creates new file if original file does exist
  createFile( copiedFileName );
  if ( fileExists(fileName) ) { // If original file exists, copy file into new file
  try {
   fileName = filePath + fileSlash + fileName;
   copiedFileName = filePath + fileSlash + copiedFileName;
   RandomAccessFile raf = new RandomAccessFile(fileName, "r");
   RandomAccessFile raf2 = new RandomAccessFile(copiedFileName, "rw");
   raf.seek( 0 );
   raf2.seek( 0 );
   Long lengthFile = new Long( raf.length() );
   byte[] b = new byte[ lengthFile.intValue() ];
   raf.readFully(b);
   raf2.write(b);
   raf.close();
  }
  catch (IOException e) {
   System.out.println("Error opening file: " + e);
  }
  }
 } // Ends copyFile
 /**
 * Searches for a partial string at the beginning of a new line
 * in a file name. For instance, searching for "ABC" in a file
 * with the line "ABCDEFGHIJKL" will return TRUE, but searching
 * for "BCD" will not return TRUE.
 *
 * Does not assume lines are in alphabetical order.
 *
 * @param fileName Name of the file to be searched
 * @param searchString Partial string to be searching for.
 * @return  TRUE if there is a match for the string being
 *    searched for, FALSE if there is no match.
 * @see   RandomAccessFile
 * @since  JDK1.3
 */
 public boolean searchForString(String fileName, String searchString) {
  int i;
  long filePointer;
  boolean stringFound = false;
  fileName = filePath + fileSlash + fileName;
  try {
  RandomAccessFile raf = new RandomAccessFile(fileName, "rw");
  raf.seek( 0 ); // Starts at the beginning of the file
  String thisString = new String();
  do {
   thisString = raf.readLine();
   if ( thisString.length() > searchString.length() )
    thisString = thisString.substring( 0, searchString.length() );
   i = searchString.compareToIgnoreCase( thisString );
   if ( i == 0 )
    stringFound = true;
  } while ( raf.getFilePointer() < raf.length() );
  raf.close();
  }
  catch (IOException e) {
  System.out.println("Error opening file: " + e);
  }
  return stringFound;
 } // ends searchForString
 /**
 * Returns the number of lines in a given file.
 *
 * @param fileName File to check for.
 * @return  The number of lines within a file.
 * @see  RandomAccessFile
 * @since  JDK1.3
 */
 public int numberOfLines( String fileName ) {
  int lineCount = 0;
  fileName = filePath + fileSlash + fileName;
  try {
  RandomAccessFile raf = new RandomAccessFile(fileName, "rw");
  raf.seek( 0 );
  if ( raf.length() > 0 ) {
   do {
    lineCount++;
    raf.readLine();
   } while ( raf.getFilePointer() < raf.length() );
  }
  raf.close();
  }
  catch (IOException e) {
  System.out.println("Error opening file: " + e);
  }
  return lineCount;
 } // end lineCount
 /**
 * Returns the full string of a partial search. For example
 * returnFullString( "jjh0901.txt", "abc" ) will return
 * "abcFullLine".
 *
 * @param fileName Name of the file.
 * @param searchString The partial string to serach for.
 * @return  The full string of the partial string being
 *    searched for.
 * @see   RandomAccessFile
 * @see   #searchForString
 * @since   JDK1.3
 */
 public String returnFullString(String fileName, String searchString) {
 // Will search for a partial string matching the BEGINNING of a new line.
 // If the string is found, will return the FULL string
  int i;
  long filePointer;
  boolean stringFound = searchForString( fileName, searchString );
  String possString = "QUACK"; // "False" data...
  if ( stringFound ) {
  try {
   fileName = filePath + fileSlash + fileName;
   RandomAccessFile raf = new RandomAccessFile(fileName, "rw");
   raf.seek( 0 );
   String thisString = new String();
   do {
    thisString = raf.readLine();
    possString = thisString.toString();
    if ( searchString.length() < thisString.length() )
    thisString = thisString.substring( 0, searchString.length() );
    i = searchString.compareToIgnoreCase( thisString );
    if ( i == 0 )
    break;
   } while ( raf.getFilePointer() < raf.length() );
   raf.close();
  }
  catch (IOException e) {
   System.out.println("Error opening file: " + e);
  }
  }
  return possString;
 } // ends returnFullString
 /**
 * Returns the end char of a line in the file. Will accept partial
 * string as a parameter. For example "abc" in a file with the line
 * "abcdefghi" will return the char 'i'.
 *
 * @param fileName Name of the file.
 * @param searchString The user's password being authenticated.
 * @return  The last char in the line being searched for.
 * @see   RandomAccessFile
 * @see    #searchForString
 * @since  JDK1.3
 */
 public char retrieveEndLineChar(String fileName, String searchString) {
 // Retrieves the end character of a line...
  int i;
  char c = '9';
  boolean stringFound = searchForString( fileName, searchString );
  if ( stringFound ) {
  try {
   fileName = filePath + fileSlash + fileName;
   RandomAccessFile raf = new RandomAccessFile(fileName, "rw");
   raf.seek( 0 );
   String thisString = new String();
   String thisSubString = new String();
   do {
    thisString = raf.readLine();
    thisSubString = thisString.toString();
    thisSubString = thisSubString.substring( 0, searchString.length() );
    i = searchString.compareToIgnoreCase( thisSubString );
    if ( i == 0 )
    c = thisString.charAt( thisString.length() - 1 );
   } while ( raf.getFilePointer() < raf.length() );
   raf.close();
  }
  catch (IOException e) {
   System.out.println("Error opening file: " + e);
  }
  }
  return c;
 } // ends retriveEndLineChar
 /**
 *
 *
 * @param fileName Name of the file to insert the line into.
 * @param dataToInsert Data to insert.
 * @see   RandomAccessFile
 * @since  JDK1.3
 */
 public void writeIntoFile (String fileName, String dataToInsert) {
 // Appends a string to the end of the file.
 // Assumes the last character is a line break.
  int i = 360;
  long filePointer;
  boolean iReachesZero = false;
  fileName = filePath + fileSlash + fileName;
  try {
  RandomAccessFile raf = new RandomAccessFile(fileName, "rw");
  filePointer = raf.length();
  raf.seek( filePointer );
  raf.writeBytes( dataToInsert + "\n"); // inserts the data plus a line break
  raf.close();
  }
  catch (IOException e) {
  System.out.println("Error opening file: " + e);
  }
 } // ends writeIntoFile
 /**
 * Inserts a line into the file in alphabetical order.
 *
 * @param fileName Name of the file to insert the line into.
 * @param dataToInsert Data to insert.
 * @see   RandomAccessFile
 * @since  JDK1.3
 */
 public void insertIntoFile(String fileName, String dataToInsert) {
 // Inserts a string into the file in alphabetical order.
  int i = 360;
  long filePointer;
  boolean iReachesZero = false;
  fileName = filePath + fileSlash + fileName;
  try {
  RandomAccessFile raf = new RandomAccessFile(fileName, "rw");
  raf.seek( 0 );
  filePointer = 0;
  String thisString = new String();
  do {
   if ( raf.getFilePointer() < raf.length() ) {
    thisString = raf.readLine();
    i = dataToInsert.compareToIgnoreCase( thisString );
   }
   if ( i == 0 )
    iReachesZero = true;
   if ( i > 0 )
    filePointer = raf.getFilePointer();
  } while ( raf.getFilePointer() < raf.length() );
  if ( !iReachesZero ) {
   raf.seek( filePointer );
   Long lengthPos = new Long( raf.length() - raf.getFilePointer() );
   byte[] b;
   b = new byte[ lengthPos.intValue() ];
   raf.readFully(b);
   raf.seek( filePointer );
   raf.writeBytes( dataToInsert + "\n"); // inserts the data plus a line break
   raf.write(b);
  }
  raf.close();
  }
  catch (IOException e) {
  System.out.println("Error opening file: " + e);
  }
 } // Ends insertIntoFile
 /**
 * Deletes a line from the file. Will only accept full
 * lines (not partial lines) or the whole thing will
 * be screwed up.
 *
 * @param fileName Name of the file.
 * @param dataToDelete Data string to be deleted.
 * @see   RandomAccessFile
 * @see    #searchForString
 * @since  JDK1.3
 */
 public void deleteFromFile(String fileName, String dataToDelete) {
  int i = 360;
  long filePointer;
  long filePointer2;
  boolean iReachesZero = false;
  if ( searchForString( fileName, dataToDelete ) ) {
  try {
   fileName = filePath + fileSlash + fileName;
   RandomAccessFile raf = new RandomAccessFile(fileName, "rw");
   raf.seek( 0 );
   filePointer = 0;
   filePointer2 = 0;
   String thisString = new String();
   do {
    if ( raf.getFilePointer() < raf.length() ) {
    thisString = raf.readLine();
    i = dataToDelete.compareToIgnoreCase( thisString );
    }
    if ( i == 0 ) {
    iReachesZero = true;
    filePointer2 = raf.getFilePointer();
    }
    if ( i > 0 )
    filePointer = raf.getFilePointer();
   } while ( raf.getFilePointer() < raf.length() );
   if ( iReachesZero ) {
    raf.seek( filePointer2 );
    Long lengthPos = new Long( raf.length() - filePointer2 );
    long newLength = raf.length() - filePointer2 + filePointer;
    byte[] b;
    b = new byte[ lengthPos.intValue() ];
    raf.readFully(b);
    raf.seek( filePointer );
    raf.write(b);
    raf.setLength( newLength );
   }
   raf.close();
  }
  catch (IOException e) {
   System.out.println("Error opening file: " + e);
  }
  }
 } // Ends deleteFromFile
 /**
 * Returns the nth line in a file in String format.
 *
 * @param fileName File to browse in.
 * @param whichLine The line number to lift the string from.
 * @return  The line contents in String format.
 * @see  RandomAccessFile
 * @since  JDK1.3
 */
 public String getLine( String fileName, int whichLine ) {
  int lineCount = 0;
  String thisString = "";
  fileName = filePath + fileSlash + fileName;
  try {
  RandomAccessFile raf = new RandomAccessFile(fileName, "rw");
  raf.seek( 0 );
  if ( raf.length() > 0 ) {
   do {
    lineCount++;
    thisString = raf.readLine();
   } while ( ( raf.getFilePointer() < raf.length() ) && ( lineCount < whichLine ) );
  }
  raf.close();
  }
  catch (IOException e) {
  System.out.println("Error opening file: " + e);
  }
  return thisString;
 } // Ends getLine
 // Directory where you want to keep your files in.
 private String filePath = "C:\\jakarta-tomcat-3.2.3\\webapps\\ROOT";
 // The "slash" in file organization in your computer...
 // WINDOWS USERS: Should stay "\\".
 // LINUX USERS: Should amend to "/".
 private String fileSlash = "\\";
} // Ends UniversalFileHandler class
// Written by Jennica Humphrey
// (emelia2002@hotmail.com)
// Free for redistribution as long as you keep the credits and comments unchanged!
```

