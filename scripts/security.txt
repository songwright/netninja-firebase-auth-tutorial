// This is a copy of the Firebase security rules for this database.
// This script does not run on this page. It is here:
// https://console.firebase.google.com/project/netninja-firebase-auth-tut/database/firestore/rules

service cloud.firestore {
  match / databases / { database } / documents {

    // match logged in user doc in users collection
    match / users / { userID } {
      allow create: if request.auth.uid != null;
      allow read: if request.auth.uid == userID;
    }

    // match docs in the guides collection
    // If a logged on user exists, allow read & write.
    match / guides / { guideID } {
      allow read, write: if request.auth.uid != null;
    }
  }
}

// For this tutorial the credentials are:
// username: mario@thenetninja.co.uk
// password: test1234