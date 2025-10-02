<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Phrases App</title>
</head>
<body>
  <h1>My Phrases</h1>

  <input type="text" id="phraseInput" placeholder="Enter a phrase" />
  <button onclick="savePhrase()">Save</button>

  <h2>Saved Phrases:</h2>
  <ul id="phrasesList"></ul>

  <script type="module">
    import { createClient } from "https://cdn.jsdelivr.net/npm/@supabase/supabase-js/+esm";

    // ✅ Your real Supabase details
    const SUPABASE_URL = "https://qrxiyoisqngsjgydqvwi.supabase.co";
    const SUPABASE_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InFyeGl5b2lzcW5nc2pneWRxdndpIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTkzODQ5OTEsImV4cCI6MjA3NDk2MDk5MX0.rP6fhbyicfw6AeSkKXjmL-URA_Ph3xplAzX4sDoAYVs";

    const supabase = createClient(SUPABASE_URL, SUPABASE_KEY);

    async function savePhrase() {
      const input = document.getElementById("phraseInput");
      const phrase = input.value;

      if (!phrase) return alert("Please enter a phrase!");

      const { error } = await supabase.from("phrases").insert([{ phrase }]);
      if (error) {
        alert("Error: " + error.message);
      } else {
        alert("Saved!");
        input.value = "";
        loadPhrases();
      }
    }

    async function loadPhrases() {
      const { data, error } = await supabase
        .from("phrases")
        .select("*")
        .order("id", { ascending: false });

      if (error) {
        console.error(error);
        return;
      }

      const list = document.getElementById("phrasesList");
      list.innerHTML = "";
      data.forEach(row => {
        const li = document.createElement("li");
        li.textContent = row.phrase;
        list.appendChild(li);
      });
    }

    document.addEventListener("DOMContentLoaded", loadPhrases);
  </script>
</body>
</html>
