<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Contact Us</title>

<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #f5f5f5;
    }

    .container {
        width: 500px;
        margin: 40px auto;
        background: #fff;
        padding: 20px;
        border: 1px solid #ccc;
    }

    h2 {
        margin-bottom: 20px;
    }

    label {
        display: block;
        margin-top: 10px;
        font-weight: bold;
    }

    input[type="text"], textarea, select {
        width: 100%;
        padding: 8px;
        margin-top: 5px;
        border: 1px solid #ccc;
    }

    textarea {
        height: 100px;
    }

    .radio-group {
        margin-top: 5px;
    }

    .radio-group input {
        margin-left: 5px;
    }

    button, input[type="submit"] {
        margin-top: 15px;
        padding: 8px 15px;
        cursor: pointer;
    }

    .error {
        color: red;
        margin-top: 10px;
    }

    .preview {
        margin-top: 20px;
        padding: 10px;
        border: 1px solid #000;
        background: #fafafa;
    }
</style>

<script>
function validateForm() {
    let name = document.getElementById("name").value.trim();
    let email = document.getElementById("email").value.trim();
    let phone = document.getElementById("phone").value.trim();
    let message = document.getElementById("message").value.trim();

    let error = document.getElementById("error");
    error.innerHTML = "";

    let emailPattern = /^[^ ]+@[^ ]+\.[a-z]{2,3}$/;
    let phonePattern = /^[0-9]{10}$/;

    if (name === "" || email === "" || phone === "" || message === "") {
        error.innerHTML = "All fields are required.";
        return false;
    }

    if (!email.match(emailPattern)) {
        error.innerHTML = "Please enter a valid email.";
        return false;
    }

    if (!phone.match(phonePattern)) {
        error.innerHTML = "Phone number must be exactly 10 digits.";
        return false;
    }

    return true;
}

function previewData() {
    let name = document.getElementById("name").value;
    let email = document.getElementById("email").value;
    let phone = document.getElementById("phone").value;
    let message = document.getElementById("message").value;

    let contact = document.querySelector('input[name="contact"]:checked');
    let inquiry = document.getElementById("inquiry").value;

    document.getElementById("preview").innerHTML = `
        <h3>Preview (GET Method)</h3>
        <p><b>Name:</b> ${name}</p>
        <p><b>Email:</b> ${email}</p>
        <p><b>Phone:</b> ${phone}</p>
        <p><b>Message:</b> ${message}</p>
        <p><b>Preferred Contact:</b> ${contact ? contact.value : ""}</p>
        <p><b>Inquiry Type:</b> ${inquiry}</p>
    `;
}
</script>

</head>

<body>

<div class="container">

<h2>Contact Us</h2>

<p id="error" class="error"></p>

<form action="server.php" method="POST" onsubmit="return validateForm()">

<label>Name:</label>
<input type="text" id="name" name="name">

<label>Email:</label>
<input type="text" id="email" name="email">

<label>Phone Number:</label>
<input type="text" id="phone" name="phone">

<label>Message:</label>
<textarea id="message" name="message"></textarea>

<label>Preferred Contact Method:</label>
<div class="radio-group">
    <input type="radio" name="contact" value="Email"> Email
    <input type="radio" name="contact" value="Phone"> Phone
    <input type="radio" name="contact" value="Both"> Both
</div>

<label>Inquiry Type:</label>
<select id="inquiry" name="inquiry">
    <option value="">Select an option</option>
    <option value="General Inquiry">General Inquiry</option>
    <option value="Support Request">Support Request</option>
    <option value="Feedback">Feedback</option>
</select>

<button type="button" onclick="previewData()">Preview (GET)</button>

<input type="submit" value="Submit">

</form>

<div id="preview" class="preview"></div>

</div>

</body>
</html>
