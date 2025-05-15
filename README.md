## Project Architecture

///نحتاج واجهة امامية وواجهة خلفية لمشروعناا


## FrontEnd:
React or  لإنشاء واجهة تفاعلية من اجل تصفح المتجر 
next js  or
html - css - javascrirt (pure)

## BackEnd
Node js  بناء الخادم
MongoDb للتعامل مع قاعدة بيانات MongoDB.


## Libraries :
- Express  ////  framework لتسهيل بناء apis
- morgan  /////    Middleware (برمجية وسيطة) يستخدم مع Express لتسجيل معلومات الطلبات الواردة إلى الخادم.
- nodemon  ///   أداة تستخدم لمراقبة تغييرات الملفات في مشروع Node.js.
- dotenv  //////////    مكتبة صغيرة لتحميل المتغيرات البيئية 

## Project Structure:
Task4:
|--->petsStore      
    |->node_module
    |->.env       رقم البورت المستخدم لدي
    |->.gitignore     الملفات التي لا اريد رفعها الى github
    |-README.md
    |-> src
        |-->config
        |-->routes
            |--pets.route.js     (الراوتر الخاص بالحيوانات)
            |--users.route.js     (الراوتر الخاص بالمستخدمين)
            |--clinic.route.js     (الراوتر الخاص بالعيادة)
            |--article.route.js     (الراوتر الخاص بالمقالات)
        |-->controllers
            |--pets.controller.js   (التحكم بال api الخاص  بالحيوانات)
            |--users.controller.js   (التحكم بال api الخاص بالمستخدم)
            |--clinic.route.js     (التحكم ب api الخاص بالعيادة)
            |--article.route.js     (الاتحكم بال api الخاص بالمقالات)
        |-->models
        |-->middlewares
            |-->params
        |-->app.js      الملف الاساسي للشروع
        |-->server.js    السيرفر الذي سوف استخدمه
        |--data
            |--petsData
            |--clinicData
            |--articleData

## APIS:

### 1. GET pets  

Get : 'api/pets'

method : get
response : رسالة نجاح العملية والداتا الخاصة بالحيوانات

body : لا يحتاج
query : نعم نحتاج لنقوم بال filter حسب الشروط الموجودة
Params: 
  - type
  - location

-Response Example  اعادة كل الحيوانات
data:
[
  {
    "id": 1,
    "name": "Max",
    "type": "Dog",
    "age": 3,
    "location": "Roma",

  } ,
  {
    "id": 2,
    "name": "Sona",
    "type": "Cat",
    "age": 3 ,
    "location": "Milano",

  } ,
  {
    "id": 3,
    "name": "Ghost",
    "type": "Dog",
    "age": 1 ,
    "location": "Roma",

  } ,
]
Expected Errors:
اختيار نوع غير موجود او موقع غير موجود في الداتا لدي


### 2. search on pets (by location or type)
هنا نبحث عن الحيوانات حسب شروط مثو النوع الذي اريده كلب لا  الموقع في روما 
if (type ==dog && location= "..." ) 
Get : 'api/pets ?location = roma&type = "dog" '

method : get
response : رسالة نجاح العملية والداتا الخاصة بالحيوانات

-Response Example:
data:
[
  {
    "id": 1,
    "name": "Max",
    "type": "Dog",
    "age": 3,
    "location": "Roma",

  } ,
  {
    "id": 3,
    "name": "Ghost",
    "type": "Dog",
    "age": 1 ,
    "location": "Roma",

  } ,
]


//// البحث عن عيادات بيطرية 
3. GET /clincs (api/clinic)
Get : 'api/clinics'

method : get
response : رسالة نجاح العملية والداتا الخاصة بالعيادات

body : لا يحتاج

query : نعم لاننا سنضع شرط اذا كانت العيادة للطوارئ يقوم ب filter واذا ليست للطوارئ يعيد كل العيادات

- Params
  - location (required)
  - isEmergency (optionals)  ( ا هل العيادة للطوارئ ام لا ) 


- Response Example:
اذا العيادة ليست للطوارئ يعيد كل شيء
data:
[
  {
    id:1 ,
    "name": "Happy Clinic",
    "location": "https://maps.google.com..",
    "isOpenNow": true,
    "emergencyAvailable": true
  },
  {
    id:2 ,
    "name": "Pest Clinic",
    "location": "https://maps.google.com..",
    "isOpenNow": false,
    "emergencyAvailable": false
  },
  {
    id:3 ,
    "name": "Paris Clinic",
    "location": "https://maps.google.com..",
    "isOpenNow": true,
    "isImergecy": true
  },
]

Expected Errors:
عدم إرسال loction = خطأ 400.
إحداثيات غير صحيحة (  الموقع غير موجود ضمن البلد).
عدم وجود اية عيادة للطوارئ


////فقط للطوارئ البحث عن عيادات بيطرية  وموقعها قريب

4. GET /clincs/isImergency&&location=""
نضع شرط ان يكون ال isImergency =true  , الموقع محدد
Get : 'api/clinics/isImergency="true && location = "" '

method : get
response :وموقعها قريب رسالة نجاح العملية والداتا الخاصة بالعيادات للطوارئ فقط

- Response Example:
data:
[
  {
    id:1 ,
    "name": "Happy Clinic",
    "location": "https://maps.google.com..",
    "isOpenNow": true,
    "emergencyAvailable": true
  },
  {
    id:3,
    "name": "Paris Clinic"
    "location": "https://maps.google.com..",
    "isOpenNow": true,
    "emergencyAvailable": true
  },
]



///جميع المقالات
5. GET /articles

Get : 'api/article/'

method : get
response : رسالة نجاح العملية والداتا الخاصة بالمقالات

body : لا يحتاج
query : حسب الشرط لدسنا حيث شنقوم بفلترة اذا كان النوع محدد واذا لم نحدد النوع سيعيد كل الحيوانات
Params:
-- type اذا كان كلب او قطة مثل 

data:
[
  {
    "title": "How to Take Care of Your Dog",
    "summary": "Basic dog care tips...",
    "url": "https://articles.com/dog-care" ,
    type :"dog"
  },
  {
    "title": "How to Take Care of Your Dog",
    "summary": "Basic dog care tips...",
    "url": "https://articles.com/dog-care" ,
    type :"cat"
  },
]

Expected Errors:
وضع نوع غير موجود مثل fish 


///حسب النوع المقالات
5. GET /articles/typr="dog"

method : get
response : رسالة نجاح العملية والداتا الخاصة بالمقالات فقط حسب النوع


data::
[
  {
    "title": "How to Take Care of Your Dog",
    "summary": "Basic dog care tips...",
    "url": "https://articles.com/dog-care" ,
    type :"dog"
  },
]






المشروع يكون فيه ايضا واجهة Admin ويستطيع ان يقزم بالاضافة والحذف والتعديل 

في الاضافة :
method : post
response :مع الاضافة رسالة نجاح العملية والداتا  

body : نضيف ال json وتكون تحتوي على :
  {
    "id": 1,
    "name": "Max",
    "type": "Dog",
    "age": 3,
    "location": "Roma",
  } ,
- query : لا يوجد
- Params : لا يوجد


في التعديل :
method : put
ويكون التعديل حسب ال id 
respon : يعيد رسالة مع المصفوفة بعد التعديل
- query : لا يوجد
- Params : id
body : نضيف ال json وتكون تحتوي على :
  {
    "id": 1,
    "name": "Max",
    "type": "Dog",
    "age": 3,
    "location": "Roma",
  } ,




في الحذف :
method : delete
params : id
