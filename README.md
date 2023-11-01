# API
1. GraphQL
2. SOAP
3. REST
4. gRPC
## Authentication Types
1. No Authentication (Rate Limit)
2. Basic Authentication (Base64)
3. API Key Authorisation
4. Token Based Authentication (OAuth 2.0)
## Using https
```
import https from "https";

app.get("/", (req, res) => {
  const options = {
    hostname: "bored-api.appbrewery.com",
    path: "/random",
    method: "GET",
  };

  const request = https.request(options, (response) => {
    let data = "";
    response.on("data", (chunk) => {
      data += chunk;
    });

    response.on("end", () => {
      try {
        const result = JSON.parse(data);
        res.render("index.ejs", {activity: data})
    } catch (error) {
      console.error("Failed to parse response:", error.message);
      res.status(500).send("Failed to fetch activity. Please try again.");
    }
  });
});

  request.on("error", (error) => {
    console.log("Failed to make request:", error.message);
    res.status(500).send("Failed to fetch activity. Please try again.");
  });
  request.end();
});
```
## Using axios
### ES6
```
import axios from "axios";

axios
  .get("URL", {
    params: {
      ID: 12345,
    },
  })
  .then(function (response) {
    res.json({ data: response.data });
  })
  .catch(function (error) {
   res.status(404).send(error.response.data);
  })
```
### ES7
```
import axios from "axios";

app.get("/", async (req, res) => {
  try {
    const response = await axios.get("https://bored.api.appbrewery.com/random");
    res.render("index.ejs", { activity: response.data });
  } catch (error) {
    console.error("Failed to make request:", error.message);
    res.status(500).send("Failed to fetch activity. Please try again.");
  }
});
```
