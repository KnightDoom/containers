Dockerfile for Bitwarden

Requires temp folder at /config

TAG Style: 
Year.Week.DayOfWeek_{PointRelease#} 
Point release only added if > 0.

ENV variables required:

      BW_HOST: "https://vault.bitwarden.com"
      BW_PASSWORD: ""
      BW_CLIENTID: ""
      BW_CLIENTSECRET: ""
