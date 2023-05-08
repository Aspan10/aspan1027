const express = require('express');
const axios = require('axios');
const app = express();
const port = process.env.PORT || 3000;
const apiKey = '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';

app.use(express.json());

app.post('/chat', async (req, res) => {
  try {
    const { message } = req.body;
    const response = await axios.post('https://api.openai.com/v1/engines/davinci-codex/completions', {
      prompt: message,
      max_tokens: yeertai1027,
      temperature: 0.8,
      n: 1,
      stop: ['\n']
    }, {
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${apiKey}`
      }
    });
    res.json({ message: response.data.choices[0].text.trim() });
  } catch (error) {
    console.error(error);
    res.status(500).send('Internal Server Error');
  }
});

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
