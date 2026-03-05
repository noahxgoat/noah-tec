<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Noah AI</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 50px;
      background-color: #f5f5f5;
    }
    input {
      width: 60%;
      padding: 10px;
      font-size: 16px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      margin-left: 10px;
      cursor: pointer;
    }
    #response {
      margin-top: 30px;
      font-size: 18px;
      color: #333;
    }
  </style>
</head>
<body>
  <h1>Noah AI Tech</h1>
  <input type="text" id="prompt" placeholder="Type your question here..." />
  <button onclick="askAI()">Ask</button>
  <div id="response"></div>

  <script>
    const API_TOKEN = "YOUR_HUGGING_FACE_TOKEN"; // Replace with your token
    const MODEL = "YOUR_MODEL_NAME"; // Replace with your Hugging Face model

    async function askAI() {
      const prompt = document.getElementById('prompt').value;
      if (!prompt) return;
      const responseDiv = document.getElementById('response');
      responseDiv.innerHTML = "Noah AI is thinking... 🤖";

      try {
        const res = await fetch(`https://api-inference.huggingface.co/models/${MODEL}`, {
          method: "POST",
          headers: {
            "Authorization": `Bearerhf_ztfghjnUYktPhGzdOMdxOJKiJaBihfHQFv`,
            "Content-Type": "application/json"
          },
          body: JSON.stringify({ inputs: prompt })
        });

        const data = await res.json();
        if (data.error) {
          responseDiv.innerHTML = "Error: " + data.error;
        } else {
          // Display AI output
          responseDiv.innerHTML = data[0].generated_text || JSON.stringify(data);
        }
      } catch (err) {
        responseDiv.innerHTML = "Error: " + err.message;
      }
    }
  </script>
</body>
</html>
