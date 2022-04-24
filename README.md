# Firebase Emulator Suite

A bare-bones docker configuration for [Firebase Emulator Suite](https://firebase.google.com/docs/emulator-suite).

> The Firebase Local Emulator Suite is a set of advanced tools for developers looking to build and test apps locally using Cloud Firestore, Realtime Database, Cloud Storage, Authentication, Cloud Functions, Pub/Sub, and Firebase Hosting. It provides a rich user interface to help you get running and prototyping quickly.

## Usage

**Note:**  
The firebase emulator make use of multiple ports, see docker-compose.yml for the list of port mapping to ensure those ports are free, or change the host mappings, before continuing.

**Start docker containers with docker-compose**
```
docker-compose up -d
```

**Execute in to the firebase shell**  
All commands from this point on should be run within the firebase containers shell.
```
docker-compose exec firebase bash
```

**Login to firebase**
```
firebase login --no-localhost
```

**Initialize firebase**
```
firebase init
```
Select the features you want to emulate, note that if these features are not already enabled for your firebase project, they will be enabled if selected here. At a minimum, "Emulators" should be enabled.

**Update firebase config to use localhost**  
Edit `/firebase/emulators/firebase.json` to use `0.0.0.0` as the host for each emulator. For example -
```
{
  "functions": {
    "predeploy": [
      "npm --prefix \"$RESOURCE_DIR\" run lint"
    ]
  },
  "storage": {
    "rules": "storage.rules"
  },
  "emulators": {
    "auth": {
      "host": "0.0.0.0",
      "port": 9099
    },
    "functions": {
      "host": "0.0.0.0",
      "port": 5001
    },
    "firestore": {
      "host": "0.0.0.0",
      "port": 8080
    },
    "database": {
      "host": "0.0.0.0",
      "port": 9000
    },
    "hosting": {
      "host": "0.0.0.0",
      "port": 5000
    },
    "pubsub": {
      "host": "0.0.0.0",
      "port": 8085
    },
    "storage": {
      "host": "0.0.0.0",
      "port": 9199
    },
    "ui": {
      "host": "0.0.0.0",
      "enabled": true,
      "port": 4000
    }
  }
}
```

**Start emulators**
```
firebase emulators:start
```

You should now be able to access the Firebase emulator UI at [http://localhost:4000](http://localhost:4000).

For more information on the Firebase emulator, [view the docs](https://firebase.google.com/docs/emulator-suite).