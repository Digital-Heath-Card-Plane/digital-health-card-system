# বাংলাদেশ ডিজিটাল হেলথ কার্ড সিস্টেম (Bangladesh Digital Health Card System) - মনোরেপো

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) <!-- প্রয়োজন অনুযায়ী লাইসেন্স পরিবর্তন করুন -->
[![CI Status](https://github.com/Digital-Heath-Card-Plane/digital-health-card-system/actions/workflows/ci.yml/badge.svg)](https://github.com/Digital-Heath-Card-Plane/digital-health-card-system/actions/workflows/ci.yml) <!-- CI Workflow ফাইলের সঠিক পাথ দিন -->

দেশের সকল নাগরিকের জন্য একটি সমন্বিত ডিজিটাল স্বাস্থ্য তথ্য ব্যবস্থা তৈরির লক্ষ্যে বাংলাদেশ ডিজিটাল হেলথ কার্ড সিস্টেম প্রকল্পটি গ্রহণ করা হয়েছে। এই মনোরেপোটিতে প্রকল্পের সমস্ত সোর্স কোড, অ্যাপ্লিকেশন, সার্ভিস, লাইব্রেরি এবং ডকুমেন্টেশন অন্তর্ভুক্ত রয়েছে।

**প্রযুক্তি স্ট্যাক:** JavaScript/TypeScript, Node.js, React, React Native, PostgreSQL, MongoDB, Docker, Kubernetes, Turborepo, PNPM। 

**Monorepo Management Tool:** [Turborepo](https://turbo.build/)
**Package Manager:** [PNPM](https://pnpm.io/)

## 🚀 শুরু করুন (Getting Started)

এই মনোরেপোটি ডেভেলপমেন্টের জন্য সেটআপ করতে নিচের ধাপগুলো অনুসরণ করুন:

**পূর্বশর্ত (Prerequisites):**

*   [Node.js](https://nodejs.org/) (ভার্সন 18.x বা তার উপরে, `.nvmrc` ফাইল থাকলে `nvm use` ব্যবহার করুন)
*   [PNPM](https://pnpm.io/installation) (ভার্সন 8.x বা তার উপরে)
*   [Docker](https://www.docker.com/get-started) এবং Docker Compose (লোকালে ডেটাবেস বা অন্যান্য সার্ভিস চালানোর জন্য)
*   [Git](https://git-scm.com/)

**সেটআপ (Setup):**

1.  **রিপোজিটরি ক্লোন করুন:**
    ```bash
    git clone https://github.com/Digital-Heath-Card-Plane/digital-health-card-system.git
    cd digital-health-card-system
    ```

2.  **ডিপেন্ডেন্সি ইনস্টল করুন:**
    মনোরেপোর রুট ডিরেক্টরি থেকে PNPM ব্যবহার করে সকল ওয়ার্কস্পেসের ডিপেন্ডেন্সি ইনস্টল করুন:
    ```bash
    pnpm install
    ```
    এটি সকল `apps/*`, `services/*`, এবং `libs/*` এর জন্য প্রয়োজনীয় নোড মডিউল ইনস্টল করবে।

3.  **এনভায়রনমেন্ট ভ্যারিয়েবল সেটআপ (.env):**
    *   প্রয়োজনীয় সার্ভিস বা অ্যাপ্লিকেশনের (`apps/*`, `services/*`) রুটে `.env.example` ফাইল থাকতে পারে। সেটিকে কপি করে `.env` ফাইল তৈরি করুন এবং প্রয়োজনীয় ভ্যারিয়েবলগুলো (যেমন: ডেটাবেস কানেকশন স্ট্রিং, API কী) সেট করুন।
    *   উদাহরণ (`services/identity-service` এর জন্য):
        ```bash
        cp services/identity-service/.env.example services/identity-service/.env
        # এখন services/identity-service/.env ফাইলটি এডিট করুন
        ```
    *   `.env` ফাইলগুলো `.gitignore` এ যোগ করা আছে, তাই এগুলো গিট-এ কমিট হবে না।

4.  **ডেটাবেস ও অন্যান্য সার্ভিস চালু করুন (Docker Compose):**
    যদি প্রোজেক্টে ডেটাবেস (PostgreSQL, MongoDB) বা অন্যান্য প্রয়োজনীয় সার্ভিস (যেমন Redis, Kafka) লোকাল ডেভেলপমেন্টের জন্য Docker Compose ব্যবহার করে চালানো হয়:
    ```bash
    # রুট ডিরেক্টরি বা যেখানে docker-compose.yml আছে
    docker-compose up -d
    ```
    (প্রয়োজনে ডেটাবেস মাইগ্রেশন বা সিডিং স্ক্রিপ্ট চালান।)

5.  **প্রাথমিক বিল্ড (ঐচ্ছিক কিন্তু প্রস্তাবিত):**
    সকল প্যাকেজ একবার বিল্ড করে নিতে পারেন Turborepo ব্যবহার করে:
    ```bash
    pnpm run build
    ```

## 🛠️ ডেভেলপমেন্ট (Development)

Turborepo ব্যবহার করে ডেভেলপমেন্ট সার্ভার বা নির্দিষ্ট টাস্ক চালানো হয়।

*   **সকল অ্যাপ্লিকেশন ও সার্ভিসের ডেভ সার্ভার একসাথে (সমান্তরালে) চালু করতে:**
    ```bash
    pnpm run dev
    ```
    (`turbo run dev --parallel` কমান্ড ব্যবহার করবে)।

*   **নির্দিষ্ট একটি অ্যাপ্লিকেশন বা সার্ভিসের ডেভ সার্ভার চালু করতে:**
    ```bash
    # রোগীর ওয়েব পোর্টাল চালু করতে
    pnpm --filter web-patient-portal run dev

    # অথবা Turborepo এর মাধ্যমে
    turbo run dev --filter=web-patient-portal
    ```

*   **সকল প্যাকেজ বিল্ড করতে:**
    ```bash
    pnpm run build
    ```

*   **নির্দিষ্ট একটি প্যাকেজ বিল্ড করতে:**
    ```bash
    turbo run build --filter=ehr-service
    ```

*   **সকল প্যাকেজের টেস্ট চালাতে:**
    ```bash
    pnpm run test
    ```

*   **নির্দিষ্ট একটি প্যাকেজের টেস্ট চালাতে:**
    ```bash
    turbo run test --filter=identity-service
    ```

*   **সকল প্যাকেজের লিন্ট চেক করতে:**
    ```bash
    pnpm run lint
    ```


## 📁 ফোল্ডার কাঠামো (Folder Structure)

এই মনোরেপোটি নিম্নোক্ত ফোল্ডার কাঠামো অনুসরণ করে:


```bash
digital-health-card-system/
├── apps/                     # ব্যবহারকারী-মুখী অ্যাপ্লিকেশন (Frontend/Mobile)
│   ├── web-patient-portal/   # রোগীর ওয়েব পোর্টাল (e.g., React/Angular/Vue)
│   ├── web-doctor-portal/    # ডাক্তারের ওয়েব পোর্টাল
│   ├── web-admin-portal/     # অ্যাডমিন/হাসপাতাল কর্তৃপক্ষের পোর্টাল
│   └── mobile-app/           # মোবাইল অ্যাপ (e.g., React Native/Flutter)
│
├── services/                 # ব্যাকএন্ড মাইক্রোসার্ভিসেস
│   ├── identity-service/     # পরিচয় ও অ্যাক্সেস ম্যানেজমেন্ট (IAM)
│   ├── patient-service/      # রোগী/নাগরিক তথ্য ব্যবস্থাপনা
│   ├── ehr-service/          # ইলেকট্রনিক হেলথ রেকর্ড (EHR)
│   ├── eprescription-service/ # ই-প্রেসক্রিপশন
│   ├── pharmacy-service/     # ফার্মেসি ইন্টিগ্রেশন
│   ├── billing-service/      # বিলিং ও পেমেন্ট
│   ├── notification-service/ # নোটিফিকেশন (SMS, Email)
│   └── audit-service/        # অডিট ও লগিং
│
├── libs/                     # শেয়ার্ড লাইব্রেরি/প্যাকেজ
│   ├── shared-types/         # কমন ডেটা টাইপ/ইন্টারফেস (e.g., TypeScript types)
│   ├── ui-components/        # শেয়ার্ড UI কম্পোনেন্ট (যদি ফ্রন্টএন্ড একই প্রযুক্তির হয়)
│   ├── data-validators/      # শেয়ার্ড ভ্যালিডেশন লজিক
│   └── api-client/           # সার্ভিসগুলোর মধ্যে যোগাযোগের জন্য ক্লায়েন্ট লাইব্রেরি (ঐচ্ছিক)
│
├── infra/                    # ইনফ্রাস্ট্রাকচার অ্যাজ কোড (IaC)
│   ├── terraform/            # Terraform স্ক্রিপ্ট (Cloud রিসোর্স তৈরির জন্য)
│   └── kubernetes/           # Kubernetes ম্যানিফেস্ট (Deployment, Service etc.)
│
├── docs/                     # ডকুমেন্টেশন
│   ├── architecture/         # আর্কিটেকচার ডায়াগ্রাম ও সিদ্ধান্ত
│   ├── api-specs/            # OpenAPI/Swagger স্পেসিফিকেশন
│   ├── user-guides/          # ব্যবহারকারী নির্দেশিকা
│   └──adr/                   # Architecture Decision Records
│
├── tests/                    # এন্ড-টু-এন্ড (E2E) বা ইন্টিগ্রেশন টেস্ট (যদি প্রয়োজন হয়)
│   └── e2e/
│
├── .github/                  # GitHub নির্দিষ্ট কনফিগারেশন
│   ├── workflows/            # GitHub Actions CI/CD ওয়ার্কফ্লো ফাইল (.yml)
│   └── ISSUE_TEMPLATE/       # ইস্যু রিপোর্টের টেমপ্লেট
│   └── PULL_REQUEST_TEMPLATE.md # পুল রিকোয়েস্টের টেমপ্লেট
│   └── CODEOWNERS            # কোড রিভিউয়ার নির্ধারণের ফাইল
│
├── .gitignore                # গ্লোবাল গিট ইগনোর ফাইল
├── LICENSE                   # প্রকল্পের লাইসেন্স ফাইল
├── README.md                 # প্রধান README (খুব গুরুত্বপূর্ণ!)
├── package.json              # রুট package.json (যদি Node.js ভিত্তিক টুলিং ব্যবহার করা হয়)
├── pnpm-workspace.yaml # PNPM Workspace কনফিগারেশন
└── turbo.json # Turborepo কনফিগারেশন
```


প্রতিটি ফোল্ডারের বিস্তারিত বিবরণের জন্য [docs/architecture/folder-structure.md](link/to/your/doc) দেখুন (যদি থাকে)।

## 📝 ডকুমেন্টেশন (Documentation)

প্রকল্প সম্পর্কিত বিস্তারিত ডকুমেন্টেশন `docs/` ফোল্ডারে পাওয়া যাবে:

*   **আর্কিটেকচার:** `docs/architecture/`
*   **API স্পেসিফিকেশন:** `docs/api-specs/`
*   **ব্যবহারকারী নির্দেশিকা:** `docs/user-guides/`
*   **Architecture Decision Records (ADRs):** `docs/adr/`

## 🤝 অবদান রাখা (Contributing)

এই প্রকল্পে অবদান রাখতে চাইলে অনুগ্রহ করে [CONTRIBUTING.md](CONTRIBUTING.md) ফাইলটি দেখুন (যদি থাকে)। পুল রিকোয়েস্ট তৈরির আগে ইস্যু তৈরি করে আলোচনা করার অনুরোধ করা হচ্ছে।

**কোডিং স্টাইল:** [Prettier](https://prettier.io/) এবং [ESLint](https://eslint.org/) (কনফিগারেশন ফাইল দেখুন) ব্যবহার করা হয়। কমিট করার আগে ফরম্যাটিং ও লিন্টিং চেক করার অনুরোধ করা হচ্ছে।

```bash
pnpm run lint
pnpm run format
```


