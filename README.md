# Weather Watch

An Angular dashboard showing current conditions for six cities, powered by
[WeatherAPI](https://www.weatherapi.com/).

## Setup

1. **Get a free API key**
   Sign up at [weatherapi.com](https://www.weatherapi.com/signup.aspx), then copy your key from
   the dashboard.

2. **Add the key**
   Open `src/environments/environment.ts` (and `environment.prod.ts` if you'll build for
   production) and replace the placeholder:

   ```ts
   export const environment = {
     production: false,
     weatherApiKey: '2e7b761009d44c66a2f113152260109', // <-- paste your key here
     weatherApiBaseUrl: 'https://api.weatherapi.com/v1',
   };
   ```

3. **Install dependencies**

   ```bash
   npm install
   ```

4. **Run it**

   ```bash
   npm start
   ```

   Then open http://localhost:4200.

## Changing the cities

Edit the `countries` array at the top of `src/app/app.component.ts`. Each entry has:

- `countryLabel` — what's shown as the box title (e.g. `"Japan"`)
- `query` — what's sent to WeatherAPI (a capital/major city gives the most reliable match,
  e.g. `"Tokyo"`)

```ts
{ countryLabel: 'Japan', query: 'Tokyo', data: null, loading: true, error: null }
```

## How it works

- `WeatherService` (`src/app/services/weather.service.ts`) calls WeatherAPI's
  `GET /v1/current.json?key=...&q=...` endpoint.
- `AppComponent` fires one request per country in parallel on load and on **Refresh**, and
  tracks per-box loading/error state so one failed city doesn't block the others.
- If your key is missing or invalid, every box will show an error and a banner points you back
  to the config file.
