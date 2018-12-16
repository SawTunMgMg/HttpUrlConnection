# HttpUrlConnection
အားလုံး မင်္ဂလာပါ အသုံးပြုနည်းများကို အောက်မှာ လေ့လာလိုက်ပါ 

#HttpUrlConn အသုံးပြုပုံ
-----------------

၁။ Http GET request လုပ်နည်း
---------------------

public String[] Http_Get(String url)
{
String[] response = null;
try {
HttpUrlConn.sendGetRequest(url);
response = HttpUrlConn.readMultipleLinesRespone();
}
catch (Exception ex) {
ex.printStackTrace();
}
HttpUrlConn.disconnect();
return response;
}

----------------------

၂။ Http POST လုပ်နည်း
-----------------

public String[] Http_Post(String url, Map<String, String> params) {
String[] response = null;
try {
HttpUrlConn.sendPostRequest(url, params);
response = HttpUrlConn.readMultipleLinesRespone();
}
catch (Exception ex) {
ex.printStackTrace();
}
HttpUrlConn.disconnect();
return response;
}

-----------------------

၃။ File Download ချနည်း
------------------

Download ချတဲ့ ဖိုင်ကို sdcard မှာ write မှာ ဖြစ်လို့ WRITE_EXTERNAL_STORAGE Permission လိုပါမယ်။

----------------------

public boolean DownloadFile(String fileURL, String saveDir)
{
try
{
HttpUrlConn.downloadFile(fileURL, saveDir);
return true;
} catch (Exception ex) {
ex.printStackTrace(); }
return false;
}


=====================


#HttpUrlUpload အသုံးပြုပုံ
------------------

၁။ ဖိုင် Upload တင်နည်း
----------------

Upload url ထည့်ပေးရပါမယ်။ 
sdcard ပေါ်က ဖိုင်ကို read လုပ်မှာ ဖြစ်လို့ READ_EXTERNAL_STORAGE Permission 
လိုပါမယ်။

------------------

public String[] Http_Post(String url, String charset, Map<String, String> params, Map<String, String> files)
{
String charset="UTF-8";
HttpUrlUpload multipart;
try
{
multipart = new HttpUrlUpload(url, charset);

Iterator itr = params.entrySet().iterator();
while (itr.hasNext()) {
Map.Entry entry = (Map.Entry)itr.next();
multipart.addFormField(entry.getKey().toString(), 
entry.getValue().toString());
}

Iterator itr2 = files.entrySet().iterator();
while (itr2.hasNext()) {
Map.Entry entry = (Map.Entry)itr2.next();
multipart.addFilePart(entry.getKey().toString(), 
new File( entry.getValue().toString()));
}

List response = multipart.finish();
return ((String[])response.toArray());
} catch (Exception e) {
e.printStackTrace(); }
return null;
}
