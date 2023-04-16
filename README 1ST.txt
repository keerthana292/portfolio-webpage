steps------
1.create folder,in that folder index.html(html file),style.css(css file)
2-create another folder within root folder add the required media(1-background pick,2-logo,3-resume,4-one more pick to add at ABOUT ME)
3-copy the code in respective code file.
4-if the u wanna change the icons go to www.fontawesome and get the icons
5-get the details of the  entries 
  * go to google sheets 
  * in blank sheets give the  name to form.
  * go to extensions.
  * change the name to it as same as sheet name;
*delete the exsisting code and paste
var sheetName = 'Sheet1'
var scriptProp = PropertiesService.getScriptProperties()

function intialSetup () {
  var activeSpreadsheet = SpreadsheetApp.getActiveSpreadsheet()
  scriptProp.setProperty('key', activeSpreadsheet.getId())
}

function doPost (e) {
  var lock = LockService.getScriptLock()
  lock.tryLock(10000)

  try {
    var doc = SpreadsheetApp.openById(scriptProp.getProperty('key'))
    var sheet = doc.getSheetByName(sheetName)

    var headers = sheet.getRange(1, 1, 1, sheet.getLastColumn()).getValues()[0]
    var nextRow = sheet.getLastRow() + 1

    var newRow = headers.map(function(header) {
      return header === 'timestamp' ? new Date() : e.parameter[header]
    })

    sheet.getRange(nextRow, 1, 1, newRow.length).setValues([newRow])

    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'success', 'row': nextRow }))
      .setMimeType(ContentService.MimeType.JSON)
  }

  catch (e) {
    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'error', 'error': e }))
      .setMimeType(ContentService.MimeType.JSON)
  }

  finally {
    lock.releaseLock()
  }
}











****it verifies the click give permission**********
verify your account
**u will get the sheet link copy the link and add it in the script  of (     <!----------------linking with googlesheet-------->)
&&& const scriptURL ='here pastee the url';















