<img align="tight" src="https://visitor-badge.laobi.icu/badge?page_id=kkwiek132.kkwiek123" />

<h1 align="center">
    <a href="https://git.io/typing-svg">
        <img src="https://readme-typing-svg.herokuapp.com/?font=Righteous&size=35&center=true&vCenter=true&width=500&height=70&duration=4000&lines=HI+There!+👋;+I'm+Kamil+Kwiek!;" />
    </a>
  </h1>

<h3 align="center">A passionate software tester from Poland</h3>

<br/>

<div align="center">

💻 I’m looking for new challenges as a **Software Tester**
    
🧰 I can use **Jira (Trello), TestLink (TestRail, qTest), Confluence, DevTools.**

🐛 I'm good at **finding valuable bugs.**

🎲 Fun fact **Game of Thrones Night's Watch cloaks are made from Ikea rugs.**

 </div>

<div align="center">
  <a href="mailto:kkwiek05@gmail.com">
    <img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
  </a>
  <a href="https://www.linkedin.com/in/kamil-kwiek-91b887284">
     <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
  </a>
</div>

<hr/>

<h2 align="center"> 🛠️ Languages-Frameworks-Tools 🛠️</h2>
<br/>
<div align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=mysql,postman" />
</a>

# GitHub Action for generating a contribution graph with a snake eating your contributions.
name: Generate Snake

# Controls when the action will run.
on:
  schedule:
      # every 12 hours
    - cron: "0 */12 * * *"

  # This command allows us to run the Action automatically from the Actions tab.
  workflow_dispatch:
  
  # Also run on every push on the master branch
  push:
    branches:
    - main

# The sequence of runs in this workflow:
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      - name: Clone repo
        uses: actions/checkout@v3
    
      - name: Generate the snake files in './dist/'
        uses: Platane/snk@v3
        id: snake-gif
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
            dist/github-contribution-grid-snake.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9
        env:
           GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Show build status
        run: git status

      - name: Push new files to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
          commit_message: Update snake animations
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
