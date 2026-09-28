name: Auto Sync Streak Stats

on:
  schedule:
    - cron: "0 * * * *" # Auto-syncs automatically every hour
  push:
    branches:
      - main
  workflow_dispatch: # Allows 1-click instant sync anytime from Actions tab

permissions:
  contents: write

jobs:
  update-streak:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Generate Streak Stats (Zero-Cache Live Calculation)
        uses: DenverCoder1/github-readme-streak-stats@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          options: "user=ggthedeveloper&theme=tokyonight&hide_border=true&background=070e1d&ring=38bdf8&fire=38bdf8&currStreakLabel=38bdf8&timezone=Asia/Kolkata&starting_year=2025"
          path: "profile/streak.svg"

      - name: Commit and Push Updated Telemetry
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add profile/streak.svg
          git commit -m "chore(telemetry): auto-sync live contribution streak [skip ci]" || exit 0
          git push
