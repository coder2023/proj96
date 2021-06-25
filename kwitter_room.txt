
 // Your web app's Firebase configuration
 var firebaseConfig = {
  apiKey: "AIzaSyCX626EN3OKnuz2q3-VaVtIadSyo_Z5IjQ",
  authDomain: "test-63b90.firebaseapp.com",
  databaseURL: "https://test-63b90-default-rtdb.firebaseio.com",
  projectId: "test-63b90",
  storageBucket: "test-63b90.appspot.com",
  messagingSenderId: "554774476021",
  appId: "1:554774476021:web:e4f94e7116502b776441bc"
};
// Initialize Firebase
firebase.initializeApp(firebaseConfig);



  user_name = localStorage.getItem("user_name");

document.getElementById("user_name").innerHTML = "Welcome " + user_name + "!";

function addRoom()
{
  room_name = document.getElementById("room_name").value;

  firebase.database().ref("/").child(room_name).update({
    purpose : "adding room name"
  });

    localStorage.setItem("room_name", room_name);
    
    window.location = "kwitter_page.html";
}

function getData() {  firebase.database().ref("/").on('value', function(snapshot) { document.getElementById("output").innerHTML = ""; snapshot.forEach(function(childSnapshot) { childKey  = childSnapshot.key;
       Room_names = childKey;
       console.log("Room Name - " + Room_names);
      row = "<div class='room_name' id="+Room_names+" onclick='redirectToRoomName(this.id)' >#"+ Room_names +"</div><hr>";
      document.getElementById("output").innerHTML += row;
    });
  });

}

getData();

function redirectToRoomName(name)
{
  console.log(name);
  localStorage.setItem("room_name", name);
    window.location = "kwitter_page.html";
}

function logout() {
localStorage.removeItem("user_name");
localStorage.removeItem("room_name");
    window.location = "index.html";
}