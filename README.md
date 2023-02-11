cloud firestore rule:
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }
    
    match /messages/ {docId} {
    allow read: if request.auth.uid != null;
    allow create: if canCreateMessage();
    }
    
    function canCreateMessage(){
let isSignedIn = request.auth.uid !=null;
let isOwner = request.auth.uid == request.resource.data.uid;

let isNotBanned =
exists(/database/$(database)/documents/banned/$(request.auth.uid))==false;
return isSignedIn && isOwner && isNotBanned;}
  }
}

firebase function error 났을 때
1. eslint parser error: package.json 가서 "lint": "eslint"로 바꾼다 점(.) 없애고 띄워쓰기 지우기


2. hosting할 때,
firebase init 
npm run build
firebase deploy

3. functions 사용 할 때
firebase init functions
cd functions 간 다음 진행