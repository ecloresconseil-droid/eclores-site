export default async function handler(req, res) {
  if (req.method !== "POST") {
    return res.status(405).json({ error: "Method not allowed" });
  }

  const { prenom, email, profile, score, date } = req.body;

  if (!email || !prenom) {
    return res.status(400).json({ error: "Champs manquants" });
  }

  const payload = {
    email,
    attributes: {
      PRENOM: prenom,
      QUIZ_PROFIL: profile,
      QUIZ_SCORE: score,
      QUIZ_DATE: date
    },
    listIds: [10],
    updateEnabled: true
  };

  const brevoRes = await fetch("https://api.brevo.com/v3/contacts", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "api-key": process.env.BREVO_API_KEY
    },
    body: JSON.stringify(payload)
  });

  if (!brevoRes.ok) {
    const err = await brevoRes.json();
    return res.status(500).json({ error: err });
  }

  return res.status(200).json({ success: true });
}
