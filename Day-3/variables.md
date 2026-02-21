
[![LinkedIn](https://img.shields.io/badge/Connect%20with%20me%20on-LinkedIn-blue.svg)](https://www.linkedin.com/in/rohit-rawat-7383091a7/)
[![GitHub](https://img.shields.io/github/stars/AmanPathak-DevOps.svg?style=social)](http://github.com/RohitRawat891997)
[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)](https://app.docker.com/accounts/rohitrawat891997)

---

# 🧠 GitHub Actions Variables — Complete Mental Model

Variables ka use hota hai:

✅ Reusability
✅ Clean YAML
✅ Secure automation
✅ Dynamic pipelines

3 main types:

1️⃣ Workflow variables (single workflow scope)
2️⃣ Configuration variables (multiple workflows/global)
3️⃣ Context variables (GitHub metadata)

---

# ⚙️ 1️⃣ Variables for Single Workflow

👉 Ye variables sirf ek workflow YAML file ke andar use hote hain.

### 🔹 Kaise define karte hain?

`env:` keyword use hota hai.

---

## ✅ Workflow Level Variable

```yaml
name: Demo

on: push

env:
  APP_NAME: myapp
  ENVIRONMENT: dev

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo $APP_NAME
```

### 🧠 Explanation:

* `env:` workflow ke top pe define hua
* Isliye saare jobs me available hai.

---

## ✅ Job Level Variable

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    env:
      VERSION: v1
```

👉 Sirf `build` job ke andar available.

---

## ✅ Step Level Variable

```yaml
steps:
  - name: step1
    env:
      PORT: 8080
    run: echo $PORT
```

👉 Ye variable sirf us step tak limited hai.

---

### 🔥 Scope Rule (Important)

```id="flow01"
Workflow env  ➜ sab jobs me
Job env       ➜ sirf us job me
Step env      ➜ sirf us step me
```

👉 Ye interview me bahut poocha jata hai.

---

# 🌍 2️⃣ Configuration Variables (Multiple Workflows)

👉 Ye repo ya organization level variables hote hain.

Matlab:

> Ek baar define karo — multiple workflows me use karo.

---

## 🔹 Kahan create karte hain?

GitHub Repo Settings:

```
Settings ➜ Secrets and variables ➜ Actions ➜ Variables
```

Example variable:

```
DOCKER_IMAGE = rohit/app
ENVIRONMENT = production
```

---

## ✅ Workflow me kaise use kare?

```yaml
run: echo ${{ vars.DOCKER_IMAGE }}
```

👉 Note:

* `vars.` prefix use hota hai.

---

### 🧠 Real DevOps Example:

Same repo me:

* ci.yml
* deploy.yml
* scan.yml

Sabko same docker image name chahiye.

👉 Hardcode karne ki jagah config variable use karte hain.

---

### 🔥 Difference: Secrets vs Variables

| Variables          | Secrets        |
| ------------------ | -------------- |
| Non-sensitive data | Sensitive data |
| Plain text         | Encrypted      |
| vars.NAME          | secrets.NAME   |

Example:

```yaml
${{ vars.ENVIRONMENT }}
${{ secrets.DOCKER_PASSWORD }}
```

---

# 🧬 3️⃣ Context Variables (GitHub Metadata)

👉 Ye automatic variables hote hain jo GitHub khud provide karta hai.

Matlab:

> Repo, branch, actor, commit info — sab dynamic data.

---

## 🔹 Syntax:

```yaml
${{ github.<property> }}
```

---

## 🔥 Most Important Context Variables

### ✅ Repository Name

```yaml
${{ github.repository }}
```

Output:

```
RohitRawat/devops-project
```

---

### ✅ Branch Name

```yaml
${{ github.ref_name }}
```

Output:

```
main
```

---

### ✅ Commit SHA

```yaml
${{ github.sha }}
```

👉 Docker tagging me use hota hai.

---

### ✅ Actor (Who triggered workflow)

```yaml
${{ github.actor }}
```

Output:

```
RohitRawat891997
```

---

## 🧠 Real Production Example

```yaml
- run: docker build -t app:${{ github.sha }} .
```

👉 Har commit ka unique docker image banega.

---

# 🚀 Full Real DevOps Example (All Variables Together)

```yaml
name: Variable Demo

on: push

env:
  APP_NAME: myapp

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: |
          echo "Workflow Var: $APP_NAME"
          echo "Config Var: ${{ vars.DOCKER_IMAGE }}"
          echo "Branch: ${{ github.ref_name }}"
```

---

# 🧠 Easy Memory Trick (Very Important)

GitHub Variables ko 3 layer me socho:

```id="mem01"
Local Layer   ➜ env:
Global Layer  ➜ vars.
System Layer  ➜ github.
```

---

# 💎 Advanced DevOps Tips (Interview Level)

### ✅ Context variables dynamic pipelines banate hain

Example:

```yaml
if: github.ref_name == 'main'
```

👉 Deploy sirf main branch pe.

---

### ✅ Config Variables DevOps DRY principle follow karte hain

Ek change → multiple workflows update.

---

### ✅ Workflow env fast testing ke liye use karo

Production configs → repo variables me rakho.

---

# 👨‍💻 Author

**Name:** Rohit Rawat<br>
**GitHub:** [https://github.com/RohitRawat891997](https://github.com/RohitRawat891997)<br>
**LinkedIn:** [https://www.linkedin.com/in/rohit-rawat-7383091a7/](https://www.linkedin.com/in/rohit-rawat-7383091a7/)

---
