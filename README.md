<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Support Form</title>

<style>
body{
    font-family: Arial, sans-serif;
    background:#f2f2f2;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}

.container{
    background:white;
    padding:25px;
    border-radius:10px;
    width:350px;
    box-shadow:0 0 10px rgba(0,0,0,0.1);
}

h2{
    text-align:center;
}

input, textarea{
    width:100%;
    padding:10px;
    margin-top:10px;
    border:1px solid #ccc;
    border-radius:5px;
}

button{
    margin-top:15px;
    width:100%;
    padding:10px;
    border:none;
    background:#5865F2;
    color:white;
    font-size:16px;
    border-radius:5px;
    cursor:pointer;
}

button:hover{
    background:#4752C4;
}
</style>
</head>

<body>

<div class="container">
<h2>Support Request</h2>

<form id="supportForm">

<input type="text" id="name" placeholder="Your Name" required>

<input type="text" id="userid" placeholder="Your Discord ID (e.g. 1166814431826162896)" required>

<input type="text" id="subject" placeholder="Subject" required>

<textarea id="message" placeholder="Describe your issue..." rows="5" required></textarea>

<button type="submit">Send Ticket</button>

</form>
</div>

<script>

const webhookURL = "YOUR_WEBHOOK_URL_HERE";

document.getElementById("supportForm").addEventListener("submit", function(e){

e.preventDefault();

const name = document.getElementById("name").value;
const userid = document.getElementById("userid").value;
const subject = document.getElementById("subject").value;
const message = document.getElementById("message").value;

const data = {
    embeds: [{
        title: "📩 New Support Ticket",
        color: 5814783,
        fields: [
            {
                name: "Name",
                value: name,
                inline: true
            },
            {
                name: "User ID",
                value: userid,
                inline: true
            },
            {
                name: "Subject",
                value: subject
            },
            {
                name: "Message",
                value: message
            }
        ],
        timestamp: new Date().toISOString()
    }]
};

fetch(webhookURL, {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify(data)
})
.then(response => {
    alert("Support request sent!");
    document.getElementById("supportForm").reset();
})
.catch(error => {
    alert("Error sending request.");
    console.error(error);
});

});

</script>

</body>
</html>
