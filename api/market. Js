export default async function handler(req, res) {
  try {
    const { symbol = "AAPL", interval = "1day" } = req.query;

    const apiKey = process.env.TWELVE_DATA_API_KEY;

    if (!apiKey) {
      return res.status(500).json({
        error: "Twelve Data API key is not configured"
      });
    }

    const url = new URL("https://api.twelvedata.com/time_series");
    url.searchParams.set("symbol", symbol);
    url.searchParams.set("interval", interval);
    url.searchParams.set("outputsize", "100");
    url.searchParams.set("apikey", apiKey);

    const response = await fetch(url);
    const data = await response.json();

    if (!response.ok || data.status === "error") {
      return res.status(400).json(data);
    }

    return res.status(200).json(data);
  } catch (error) {
    return res.status(500).json({
      error: error.message
    });
  }
}
