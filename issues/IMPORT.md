# How to Import These Issues into GitHub

Each `.md` file in this directory is a ready-to-paste GitHub Issue.  
Follow one of the three methods below to get them into your repository.

---

## Method 1 — Manual Copy-Paste (Easiest)

1. Open **[bry-val/golang-roadmap Issues → New Issue](https://github.com/bry-val/golang-roadmap/issues/new)** in your browser.
2. Open one of the Markdown files in this folder (e.g. `week-01.md`).
3. Copy **everything below the `---` separator** in the file (the issue body).
4. Paste it into the GitHub Issue body field.
5. Set the **Title** to the value shown at the top of the file (e.g. `Week 1: Go Toolchain & Language Foundations — Feb 25–28`).
6. Set **Labels**: `phase-1` and `week-1` (create them if they don't exist yet — see *Label Setup* below).
7. Set **Milestone**: `Phase 1 — Go Foundations` (create it if needed — see *Milestone Setup* below).
8. Set **Assignee**: `bry-val`.
9. Click **Submit new issue**.
10. Repeat for every file.

---

## Method 2 — GitHub CLI (`gh`)

> Requires [GitHub CLI](https://cli.github.com/) installed and authenticated (`gh auth login`).

```bash
# Run once from the repo root to create labels and milestone
gh label create "phase-1"  --color "#0075ca" --repo bry-val/golang-roadmap
gh label create "setup"    --color "#e4e669" --repo bry-val/golang-roadmap
for i in $(seq -w 1 8); do
  gh label create "week-$i" --color "#d93f0b" --repo bry-val/golang-roadmap
done
gh api repos/bry-val/golang-roadmap/milestones \
  -f title="Phase 1 — Go Foundations" \
  -f due_on="2026-04-17T23:59:59Z"

# Then create each issue (run from the issues/ directory)
cd issues

gh issue create \
  --repo bry-val/golang-roadmap \
  --title "Project Setup: Frictionless Learning Environment" \
  --body-file 00-project-setup.md \
  --label "phase-1,setup" \
  --milestone "Phase 1 — Go Foundations" \
  --assignee bry-val

gh issue create \
  --repo bry-val/golang-roadmap \
  --title "Week 1: Go Toolchain & Language Foundations — Feb 25–28" \
  --body-file week-01.md \
  --label "phase-1,week-1" \
  --milestone "Phase 1 — Go Foundations" \
  --assignee bry-val

gh issue create \
  --repo bry-val/golang-roadmap \
  --title "Week 2: Core Data Structures — Mar 2–6" \
  --body-file week-02.md \
  --label "phase-1,week-2" \
  --milestone "Phase 1 — Go Foundations" \
  --assignee bry-val

gh issue create \
  --repo bry-val/golang-roadmap \
  --title "Week 3: Functions & Error Handling — Mar 9–13" \
  --body-file week-03.md \
  --label "phase-1,week-3" \
  --milestone "Phase 1 — Go Foundations" \
  --assignee bry-val

gh issue create \
  --repo bry-val/golang-roadmap \
  --title "Week 4: Interfaces & OOP in Go — Mar 16–20" \
  --body-file week-04.md \
  --label "phase-1,week-4" \
  --milestone "Phase 1 — Go Foundations" \
  --assignee bry-val

gh issue create \
  --repo bry-val/golang-roadmap \
  --title "Week 5: Goroutines & Channels Basics — Mar 23–27" \
  --body-file week-05.md \
  --label "phase-1,week-5" \
  --milestone "Phase 1 — Go Foundations" \
  --assignee bry-val

gh issue create \
  --repo bry-val/golang-roadmap \
  --title "Week 6: Advanced Concurrency — Mar 30–Apr 3" \
  --body-file week-06.md \
  --label "phase-1,week-6" \
  --milestone "Phase 1 — Go Foundations" \
  --assignee bry-val

gh issue create \
  --repo bry-val/golang-roadmap \
  --title "Week 7: Testing in Go — Apr 6–10" \
  --body-file week-07.md \
  --label "phase-1,week-7" \
  --milestone "Phase 1 — Go Foundations" \
  --assignee bry-val

gh issue create \
  --repo bry-val/golang-roadmap \
  --title "Week 8: Standard Library HTTP & JSON — Apr 13–17" \
  --body-file week-08.md \
  --label "phase-1,week-8" \
  --milestone "Phase 1 — Go Foundations" \
  --assignee bry-val
```

---

## Method 3 — GitHub REST API (Advanced / Automation)

```bash
REPO="bry-val/golang-roadmap"
TOKEN="<your_personal_access_token>"   # needs repo scope

create_issue() {
  local title="$1"
  local file="$2"
  local labels="$3"
  curl -s -X POST "https://api.github.com/repos/$REPO/issues" \
    -H "Authorization: token $TOKEN" \
    -H "Content-Type: application/json" \
    -d "{\"title\": \"$title\", \"body\": $(jq -Rs . < "$file"), \"labels\": $labels, \"assignees\": [\"bry-val\"]}"
}

cd issues
create_issue "Project Setup: Frictionless Learning Environment" 00-project-setup.md '["phase-1","setup"]'
create_issue "Week 1: Go Toolchain & Language Foundations — Feb 25–28" week-01.md '["phase-1","week-1"]'
create_issue "Week 2: Core Data Structures — Mar 2–6"                  week-02.md '["phase-1","week-2"]'
create_issue "Week 3: Functions & Error Handling — Mar 9–13"            week-03.md '["phase-1","week-3"]'
create_issue "Week 4: Interfaces & OOP in Go — Mar 16–20"              week-04.md '["phase-1","week-4"]'
create_issue "Week 5: Goroutines & Channels Basics — Mar 23–27"        week-05.md '["phase-1","week-5"]'
create_issue "Week 6: Advanced Concurrency — Mar 30–Apr 3"             week-06.md '["phase-1","week-6"]'
create_issue "Week 7: Testing in Go — Apr 6–10"                        week-07.md '["phase-1","week-7"]'
create_issue "Week 8: Standard Library HTTP & JSON — Apr 13–17"        week-08.md '["phase-1","week-8"]'
```

---

## Label Setup (one-time)

| Label | Colour | Use |
|-------|--------|-----|
| `phase-1` | `#0075ca` | All Phase 1 items |
| `setup`   | `#e4e669` | Project-setup issue |
| `week-1` … `week-8` | `#d93f0b` | Per-week issues |

Create labels at: **Settings → Labels → New label**.

## Milestone Setup (one-time)

1. Go to **Issues → Milestones → New milestone**.
2. Title: `Phase 1 — Go Foundations`
3. Due date: `April 17, 2026`
4. Click **Create milestone**.

## Pinning Issues (recommended)

After creating the issues, pin **Project Setup** and **Week 1** so they appear at the top of the Issues tab:

1. Open the issue.
2. Click the **⚙ gear** next to *Pin issue* in the right sidebar.
3. Click **Pin issue**.
