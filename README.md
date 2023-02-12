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


첫 번째, npx create react app 해서 프로젝트 만들고
코드 작성하고 firebase init functions해서 functions 파일 만들고
인증, 데이터베이스, 뻔션, 호스팅 연결


1. eslint parser error: package.json 가서 "lint": "eslint"로 바꾼다 점(.) 없애고 띄워쓰기 지우기


2. hosting할 때,
firebase init 
npm run build
firebase deploy

3. functions 사용 할 때
firebase init functions
cd functions 간 다음 진행