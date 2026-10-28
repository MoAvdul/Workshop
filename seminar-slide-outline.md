# DevOps, Docker, and Modern Software Delivery
### Slide outline · Hybrid (presentation + workshop) · 26 slides · target 23 min

---

## Timing at a glance

| Speaker | Role (per course instructions) | Slides | Target time |
|---|---|---|---|
| Speaker 1 | Introduction to the topic | 1–5 | 3:50 |
| Speaker 2 | Theory and core concepts | 6–11 | 5:00 |
| Speaker 3 | Practical part 1: your first container | 12–15 | 4:10 |
| Speaker 4 | Practical part 2: containerize the todo app | 16–20 | 4:20 |
| Speaker 5 | Conclusion and tools | 21–26 | 3:50 |
| Handoffs | 4 transitions × ~30 s | | 2:00 |
| **Total** | | **26** | **~23:10** |

The allowed window is 20–25 minutes. The plan leaves about 2 minutes of buffer for a slow demo or a nervous speaker. Nobody goes past 5:00; the speaker bar on screen shows each person's countdown.

**The thread through the whole talk:** a todo app with a database. Speaker 1 shows the problem it has ("it works on my machine"), Speaker 2 explains the ideas that fix it, Speakers 3 and 4 fix it live, Speaker 5 shows how it ships automatically and what to learn next.

---

## Rules for everyone writing content

1. **One idea per slide.** If a slide needs two ideas, it needs two slides, and then something else gets cut.
2. **Slide text stays short.** Aim for 30 words or fewer on screen. Everything else goes in your speaker script.
3. **Script length:** people speak about 120 words per minute. A 50-second slide gets about 100 words of script. Write it, then read it out loud with a timer.
4. **Every number or claim needs a source link** in your notes. If you can't find a source, drop the claim.
5. **Commands must be tested.** Speakers 3 and 4: run every command yourself before sending it. Copy real output, don't invent it.
6. **Send your content in this format for each slide:** title, on-screen text, speaker script, sources, and any image you want (describe it; I handle the visuals).

---

## Speaker 1 · Introduction (slides 1–5 · 3:50)

**Goal:** the audience feels the problem and knows where the talk is going.

### Slide 1 · Title (0:30)
- **On screen:** title, subtitle "From *works on my machine* to *works everywhere*", the five speaker chips, course and date.
- **Say:** short welcome and the hook: this whole site is running inside Docker containers on a laptop at Brokes' place, served live at seminar.moabdul.dev.
- **Visual:** animated title, speaker chips (same style as the Git deck).

### Slide 2 · "It works on my machine" (1:00)
- **On screen:** a short chat-style animation. You send your project to a teammate; they reply with errors: wrong Node version, database missing, different OS.
- **Say:** a relatable story. Every student has lived this with a group project.
- **Interactive:** messages appear one by one on click.

### Slide 3 · How software used to ship (1:00)
- **On screen:** the "wall" between developers and operations. Developers write code and hand it over; operations deploy it by hand.
- **Say:** releases happened rarely, deployments were manual, and when something broke each side blamed the other.
- **Visual:** animated "code thrown over the wall".

### Slide 4 · How modern teams ship (0:50)
- **On screen:** two-column comparison, old vs. modern: release frequency, manual vs. automated, big risky releases vs. small safe changes.
- **Say:** modern teams ship small changes often, with automation doing the repetitive work.
- **To research:** one real, sourced example of a company's deployment frequency (check the DORA "State of DevOps" reports or a company engineering blog).

### Slide 5 · Today's roadmap (0:30)
- **On screen:** the five sections and the promise: "By the end, you'll know how to run your first container."
- **Say:** introduce the todo app as the example used all session. Hand off to Speaker 2.

---

## Speaker 2 · Theory and core concepts (slides 6–11 · 5:00)

**Goal:** the audience understands four ideas: DevOps, CI/CD, containers, and the Docker vocabulary.

### Slide 6 · What DevOps is (0:50)
- **On screen:** DevOps = culture + practices + tools. Developers and operations share responsibility for the software from code to production.
- **Say:** where the term came from (Patrick Debois and the first DevOpsDays in 2009; verify and cite). Point out it's a way of working, and many companies also use it as a job title.

### Slide 7 · The DevOps loop (0:50)
- **On screen:** the infinity loop: plan, code, build, test, release, deploy, operate, monitor.
- **Say:** walk the loop once, and stress that it never ends: monitoring feeds the next plan.
- **Interactive:** stages light up one at a time.

### Slide 8 · CI/CD (0:50)
- **On screen:** CI = every change gets built and tested automatically. CD = tested changes get released and deployed automatically.
- **Say:** connect to the loop: CI/CD is the automation that makes the loop fast.
- **Visual:** animated pipeline: push → build → test → deploy, with a green check at each stage.

### Slide 9 · The shipping container idea (0:50)
- **On screen:** a photo of a cargo ship with standard containers.
- **Say:** before standard shipping containers (introduced by Malcolm McLean in 1956; verify and cite), every cargo type needed different handling. One standard box changed global trade. Docker does the same for software: package the app with everything it needs, and it runs the same anywhere.

### Slide 10 · Virtual machines vs. containers (0:50)
- **On screen:** side-by-side stack diagram. VM: hardware → hypervisor → full guest OS per app. Container: hardware → OS → Docker → apps sharing the host kernel.
- **Say:** containers are lighter, start in seconds, and use less memory because they don't carry a whole operating system each.
- **Accuracy note if asked:** on Windows and macOS, Docker Desktop runs containers inside a small Linux VM behind the scenes.
- **Interactive:** toggle between the two stacks.

### Slide 11 · Four words you need (0:50)
- **On screen:** Dockerfile, image, container, registry, with one line each.
  - **Dockerfile:** the recipe (a text file of build steps).
  - **Image:** the packaged result of the recipe; read-only.
  - **Container:** a running instance of an image.
  - **Registry:** where images are stored and shared (Docker Hub, GitHub Container Registry).
- **Say:** the CS analogy: an image is a class, a container is an object. One image, many containers.
- Hand off to Speaker 3: "Enough theory, let's run one."

---

## Speaker 3 · Workshop part 1: your first container (slides 12–15 · 4:10)

**Goal:** the audience sees that running a container takes one command. Brief, clear steps only, as the instructions ask.

### Slide 12 · Get Docker (0:40)
- **On screen:** three options:
  - Windows / macOS: Docker Desktop
  - Linux: Docker Engine
  - Nothing to install: GitHub Codespaces (free with the GitHub Student pack)
- **Check:** `docker --version`
- **Visual:** QR code to the starter repo.

### Slide 13 · Hello, world (1:00)
- **Command:** `docker run hello-world`
- **Say:** explain what Docker just did: it didn't find the image locally, downloaded it from Docker Hub, created a container, ran it, and the container exited.
- **Interactive:** terminal simulator with real output, then a small animation of the pull → create → run steps.

### Slide 14 · A web server in one command (1:20)
- **Command:** `docker run -d -p 8080:80 nginx`
- **Say:** explain the flags: `-d` runs it in the background; `-p 8080:80` connects port 8080 on your machine to port 80 inside the container. Open `localhost:8080` in the browser.
- **Point to make:** you just ran a real web server without installing it.
- **Interactive:** terminal simulator, then a browser mockup showing the nginx welcome page.

### Slide 15 · Survival commands + checkpoint (1:10)
- **On screen:** the five commands you need daily:
  - `docker ps` (what's running)
  - `docker logs <id>` (what it printed)
  - `docker stop <id>` (stop it)
  - `docker rm <id>` (remove it)
  - `docker images` (what images you have)
- **Say:** run through them quickly in the terminal simulator, then a short recap: "You can now run any image from Docker Hub." Hand off to Speaker 4: "Now let's package our own app."

---

## Speaker 4 · Workshop part 2: containerize the todo app (slides 16–20 · 4:20)

**Goal:** the audience sees how their own project goes into a container, and how several containers work together.

### Slide 16 · Meet the todo app (0:30)
- **On screen:** the live app embedded, plus a three-box diagram: web (React) → api (Node) → db (Postgres).
- **Say:** this is the app from Speaker 1's story. It has three parts, so it needs three containers.

### Slide 17 · The Dockerfile, line by line (1:10)
- **On screen:** the real API Dockerfile from our repo (I'll provide it), with each line highlighted in turn.
- **Say:** explain each line in plain words: start from a Node image, set a working folder, copy the dependency list, install, copy the code, open the port, start command.
- **Bonus point:** why `package.json` is copied before the rest: Docker caches that step, so rebuilds are faster.

### Slide 18 · Build and run (0:50)
- **Commands:**
  - `docker build -t todo-api .`
  - `docker run -d -p 3000:3000 todo-api`
- **Say:** `build` turns the recipe into an image; `run` starts a container from it. The API alone fails to save todos, because there's no database yet. That motivates the next slide.
- **Interactive:** terminal simulator.

### Slide 19 · Docker Compose: the whole app in one file (1:10)
- **On screen:** the real `compose.yaml` with three services (web, api, db) and one volume, highlighted section by section.
- **Command:** `docker compose up -d`
- **Say:** one file describes the whole app. One command starts everything, in the right network, talking to each other by service name.

### Slide 20 · Proof: the data survives (0:40)
- **Commands:** `docker compose down`, then `docker compose up -d`, then refresh.
- **Say:** the todos are still there because the database stores its data in a **volume**, which lives outside the container.
- **Backup:** a recorded 20-second clip in case the live demo fails.
- Hand off to Speaker 5.

---

## Speaker 5 · Conclusion and tools (slides 21–26 · 3:50)

**Goal:** connect everything, show the tools, and give the audience a concrete next step.

### Slide 21 · How this site actually ships (0:50)
- **On screen:** our real pipeline: `git push` → GitHub Actions builds the images → pushes them to GitHub Container Registry → the server pulls the new version.
- **Say:** this is CI/CD from Speaker 2, running for real on the site you're watching.
- **Visual:** the actual workflow file next to an animated pipeline.

### Slide 22 · The DevOps tools map (0:50)
- **On screen:** tools grouped by stage:
  - Code: Git, GitHub, GitLab
  - CI/CD: GitHub Actions, GitLab CI, Jenkins
  - Containers: Docker, Podman
  - Orchestration: Kubernetes
  - Infrastructure as code: Terraform, Ansible
  - Monitoring: Prometheus, Grafana
  - Cloud: AWS, Azure, Google Cloud
- **Say:** one sentence each on where it fits in the loop. Kubernetes gets one extra line: it manages many containers across many machines, the natural next step after Compose.

### Slide 23 · Tools we used to build this seminar (0:30)
- **On screen:** React + Vite, Docker, Docker Compose, nginx, Node, PostgreSQL, GitHub Actions, Cloudflare Tunnel.
- **Say:** quick tour. This covers the "tools used" part of the instructions.

### Slide 24 · Recap (0:20)
- **On screen:** three lines:
  - DevOps: ship small changes often, automatically.
  - Docker: package an app once, run it anywhere.
  - Compose: run a whole multi-part app with one command.

### Slide 25 · Your turn: the 10-minute challenge (0:40)
- **On screen:** QR code to the starter repo and three steps:
  1. Open the repo in Codespaces (or clone it).
  2. Run `docker compose up -d`.
  3. Open the app and add your first todo.
- **Say:** this is the main call to action. Everything they need is in the repo README.

### Slide 26 · Quick quiz + thank you (0:40)
- **On screen:** 3 quick questions (e.g. image vs. container, what `-p` does, why the todos survived), then team names and "Questions?".
- **Interactive:** clickable quiz with instant feedback.

---

## What I (Brokes) handle in parallel

- Design system, slide framework, speaker bar with timers, all animations and interactive components
- The todo app (web, API, database) and the real Dockerfile and `compose.yaml` shown on slides 17 and 19
- Deployment on seminar.moabdul.dev, the GitHub Actions pipeline, and the starter repo + QR codes
- Backups: static deck copy on a second host and recorded demo clips

## Deadlines (fill in)

| Item | Owner | Due |
|---|---|---|
| Slide content + scripts | Each speaker | ____ |
| Tested commands + real output | Speakers 3 & 4 | ____ |
| First full timed rehearsal | Everyone | ____ |
| Final rehearsal | Everyone | ____ |
