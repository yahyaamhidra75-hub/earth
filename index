const functions = require("firebase-functions");
const fetch = require("node-fetch");

exports.askAI = functions.https.onRequest(async (req, res) => {
  const question = req.query.q;
  if(!question) return res.status(400).send("السؤال مطلوب");

  try {
    const response = await fetch("https://api.openai.com/v1/chat/completions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": "Bearer YOUR_OPENAI_API_KEY" // ضع مفتاح OpenAI هنا
      },
      body: JSON.stringify({
        model: "gpt-3.5-turbo",
        messages: [
          {role:"system", content:"أنت يحيى أمهيضرة، مساعد تعليمي يجيب بدقة وبساطة"},
          {role:"user", content: question}
        ],
        max_tokens: 200
      })
    });

    const data = await response.json();
    const answer = data.choices[0].message.content;
    res.json({answer});
  } catch(err){
    console.error(err);
    res.status(500).json({answer:"حدث خطأ، حاول لاحقًا"});
  }
});
