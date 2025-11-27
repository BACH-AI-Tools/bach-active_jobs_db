# Active Jobs Db MCP Server

[English](./README_EN.md) | 简体中文 | [繁體中文](./README_ZH-TW.md)

## 🚀 使用 EMCP 平台快速体验

**[EMCP](https://sit-emcp.kaleido.guru)** 是一个强大的 MCP 服务器管理平台，让您无需手动配置即可快速使用各种 MCP 服务器！

### 快速开始：

1. 🌐 访问 **[EMCP 平台](https://sit-emcp.kaleido.guru)**
2. 📝 注册并登录账号
3. 🎯 进入 **MCP 广场**，浏览所有可用的 MCP 服务器
4. 🔍 搜索或找到本服务器（`bach-active_jobs_db`）
5. 🎉 点击 **"安装 MCP"** 按钮
6. ✅ 完成！即可在您的应用中使用

### EMCP 平台优势：

- ✨ **零配置**：无需手动编辑配置文件
- 🎨 **可视化管理**：图形界面轻松管理所有 MCP 服务器
- 🔐 **安全可靠**：统一管理 API 密钥和认证信息
- 🚀 **一键安装**：MCP 广场提供丰富的服务器选择
- 📊 **使用统计**：实时查看服务调用情况

立即访问 **[EMCP 平台](https://sit-emcp.kaleido.guru)** 开始您的 MCP 之旅！


---

## 简介

这是一个 MCP 服务器，用于访问 Active Jobs Db API。

- **PyPI 包名**: `bach-active_jobs_db`
- **版本**: 1.0.0
- **传输协议**: stdio


## 安装

### 从 PyPI 安装:

```bash
pip install bach-active_jobs_db
```

### 从源码安装:

```bash
pip install -e .
```

## 运行

### 方式 1: 使用 uvx（推荐，无需安装）

```bash
# 运行（uvx 会自动安装并运行）
uvx --from bach-active_jobs_db bach_active_jobs_db

# 或指定版本
uvx --from bach-active_jobs_db@latest bach_active_jobs_db
```

### 方式 2: 直接运行（开发模式）

```bash
python server.py
```

### 方式 3: 安装后作为命令运行

```bash
# 安装
pip install bach-active_jobs_db

# 运行（命令名使用下划线）
bach_active_jobs_db
```

## 配置

### API 认证

此 API 需要认证。请设置环境变量:

```bash
export API_KEY="your_api_key_here"
```

### 环境变量

| 变量名 | 说明 | 必需 |
|--------|------|------|
| `API_KEY` | API 密钥 | 是 |
| `PORT` | 不适用 | 否 |
| `HOST` | 不适用 | 否 |



### 在 Claude Desktop 中使用

编辑 Claude Desktop 配置文件 `claude_desktop_config.json`:


```json
{
  "mcpServers": {
    "active_jobs_db": {
      "command": "uvx",
      "args": ["--from", "bach-active_jobs_db", "bach_active_jobs_db"],
      "env": {
        "API_KEY": "your_api_key_here"
      }
    }
  }
}
```

**注意**: 请将 `E:\path\to\active_jobs_db\server.py` 替换为实际的服务器文件路径。


## 可用工具

此服务器提供以下工具:


### `get_jobs_7_days`

Search and retrieve jobs on title, description, location, remote, and organization. Optionally add a text or html description

**端点**: `GET /active-ats-7d`


**参数**:

- `limit` (string): You can limit the number of jobs per API call between 10 and 100. If left blank, the default value is 100 Use the offset parameter to receive the next batch of jobs

- `offset` (string): Offset allows you to paginate results. For example, if you want to retrieve 300 jobs from our api you can send 3 requests with limit=100 and offset= 0, 100, and 200. With a limit of 10, you can fetch 30 jobs using 3 requests with offset= 0, 10, and 20

- `title_filter` (string): Search on the job title. You can search like you search on Google, see the documentation for more info.

- `advanced_title_filter` (string): Advanced Title filter which enables more features like parenthesis, 'AND', and prefix searching. Can Not be used in combination with regular title_filter Phrares (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: (AI | 'Machine Learning' | 'Robotics') & !

- `location_filter` (string): Filter on location. Please do not search on abbreviations like US, UK, NYC. Instead, search on full names like United States, New York, United Kingdom. You may filter on more than one location in a single API call using the OR parameter. For example: Dubai OR Netherlands OR Belgium

- `description_filter` (string): Filter on the job description. You can search like you search on Google, see the documentation for more info.

- `advanced_description_filter` (string): Uses the same syntax as advanced_title_filter

- `organization_filter` (string): Filter on the job's company name. Only allows for exact matches. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:NVIDIA,Walmart Warning, this filter does not work for company names using parenthesis ( ) Please send us an email at remco@fantastic.jobs to receive a list of all companies in this API

- `organization_exclusion_filter` (string): Same syntax as the organization_filter. Filter out more than one company with a comma delimited list without spaces!. Requires an exact match. Use the advanced_organization_filter for more functionality

- `description_type` (string): Description Type. Leave empty to return data without job description. Option 1: 'text' Option 2: 'html'

- `remote` (string): Example value: 

- `source` (string): You may optionally filter on the source, which are the ATS platforms. Your options are:adp, applicantpro, ashby, bamboohr, breezy, careerplug, comeet, csod, dayforce, eightfold, freshteam, gem, greenhouse, gohire, hirehive, hiringthing, icims, isolved, jazzhr, jobvite, join.com, kula, lever.co, oraclecloud, paycom, paylocity, personio, phenompeople, pinpoint, polymer, recruitee, recooty, smartrecruiters, successfactors, taleo, teamtailor, taleo, trakstar, workable, workday, zoho You can search o

- `source_exclusion` (string): You can exclude one or more sources with a comma delimited list without spaces!. For example: source_exclusion:workday,greenhouse

- `date_filter` (string): ou can use this filter to return only the most recent jobs, instead of all jobs from the last 7 days. This filter is a greater than filter. For example, if today's date is 2025-01-03 and you wish to only return jobs posted in 2025, you can filter on '2025-01-01'. To include time, use the following syntax: '2025-01-01T14:00:00' Please keep in mind that the jobs posted date/time is UTC and there's a 1 to 2 hour delay before jobs appear on this API.

- `advanced_organization_filter` (string): Advanced Organization filter which enables more features like parenthesis, 'AND', and prefix searching. This filter is also useful to exclude certain organizations. Phrases (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: University & ! Harvard Will ret

- `include_ai` (string): Example value: 

- `ai_employment_type_filter` (string): BETA Feature. Filter on a specific job type as identified by our AI, the options are: FULL_TIME/PART_TIME/CONTRACTOR/TEMPORARY/INTERN/VOLUNTEER/PER_DIEM/OTHER To filter on more than one job type, please delimit by comma, like such: FULL_TIME, PART_TIME

- `ai_taxonomies_a_filter` (string): Filter the jobs on one or more top level taxonomies. You can choose from: Technology, Healthcare, Management & Leadership, Finance & Accounting, Human Resources, Sales, Marketing, Customer Service & Support, Education, Legal, Engineering, Science & Research, Trades, Construction, Manufacturing, Logistics, Creative & Media, Hospitality, Environmental & Sustainability, Retail, Data & Analytics, Software, Energy, Agriculture, Social Services, Administrative, Government & Public Sector, Art & Design

- `ai_taxonomies_a_primary_filter` (string): Filter the jobs on one or more top level primary taxonomies. This filter will filter on the primary taxonomy only (the first taxonomy in the array) You can filter on more than one taxonomy with a comma delimited list without spaces!. For example: ai_taxonomies_a_filter:Technology,Healthcare For taxonomies including &, please double-quote

- `ai_taxonomies_a_exclusion_filter` (string): Use this parameter to exclude jobs with certain top level taxonomies from the results You can filter out more than one taxonomy with a comma delimited list without spaces!. For example: ai_taxonomies_a_exclusion_filter:Technology,Healthcare For taxonomies including &, please double-quote

- `ai_work_arrangement_filter` (string): BETA Feature. Filter on a specific work arrangement identified by our AI, This is a more granular version of the 'remote' filter, which is quite broad. the options are: On-site (Job is on site only, no working from home available) Hybrid (Job is in the office with one or more days remote) Remote OK (Job is fully remote, but an office is available) Remote Solely (Job is fully remote, and no office is available) To filter on more than one job type, please delimit by comma with no space, like such:

- `ai_has_salary` (string): Example value: 

- `ai_experience_level_filter` (string): BETA Feature. Filter on a certain required experience level as identified by our AI, the options are: 0-2/2-5/5-10/10+ To filter on more than one job type, please delimit by comma with no space, like such: 0-2,2-5

- `ai_visa_sponsorship_filter` (string): Example value: 

- `include_li` (string): Example value: 

- `li_organization_slug_filter` (string): Filter on the job's company via the slug. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:netflix,walmart Only allows for exact matches, please check the exact company slug before filtering. The slug is the company specific part of the url. For example the slug in the following url is 'walmart': https://www.linkedin.com/company/walmart/ Please send us a message or email at remco@fantastic.jobs to receive a list of companies

- `li_organization_slug_exclusion_filter` (string): Similar to the slug filter, but it removes companies from the results.

- `li_industry_filter` (string): BETA Feature Filter on the organization's LinkedIn Industry. Please use the exact Industry name. This filter is case sensitive. You can filter on more than one industry with a comma-delimited list without spaces. For example: industry_filter=Accounting,Staffing and Recruiting If the industry contains a comma, please double-quote. You can find a list of industries on our website: https://fantastic.jobs/article/linkedin-industries

- `li_organization_specialties_filter` (string): BETA Feature Filter on the job's organization LinkedIn specialties, with the same syntax as our job search filters. Please note that not all companies have specialties listed on their company profile

- `li_organization_description_filter` (string): Filter on the company's description, with the same syntax as our job search filters

- `li_organization_employees_lte` (string): Use this to filter on jobs from companies less than a certain number of employees. Can be used in combination with li_organization_employees_gte. For example, if you wish to filter on small companies but want to exclude companies with just one employee, you can use the following query filter: employees_gte=1 employees_lte=200

- `li_organization_employees_gte` (string): Use this to filter on jobs from companies less than a certain number of employees. Can be used in combination with li_organization_employees_gte. For example, if you wish to filter on small companies but want to exclude companies with just one employee, you can use the following query filter: employees_gte=1 employees_lte=200

- `ai_education_requirements_filter` (string): Please contact us before using



---


### `ultra___get_modified_jobs_24h`

Search and retrieve jobs modified during the last 24h. Run this API at the same time every day to get newly modified jobs without any duplicates

**端点**: `GET /modified-ats-24h`


**参数**:

- `limit` (string): You can limit the number of jobs per API call between 10 and 100. If left blank, the default value is 100 Use the offset parameter to receive the next batch of jobs

- `offset` (string): Offset allows you to paginate results. For example, if you want to retrieve 300 jobs from our api you can send 3 requests with limit=100 and offset= 0, 100, and 200. With a limit of 10, you can fetch 30 jobs using 3 requests with offset= 0, 10, and 20

- `title_filter` (string): Search on the job title. You can search like you search on Google, see the documentation for more info.

- `advanced_title_filter` (string): Advanced Title filter which enables more features like parenthesis, 'AND', and prefix searching. Can Not be used in combination with regular title_filter Phrares (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: (AI | 'Machine Learning' | 'Robotics') & !

- `location_filter` (string): Filter on location. Please do not search on abbreviations like US, UK, NYC. Instead, search on full names like United States, New York, United Kingdom. You may filter on more than one location in a single API call using the OR parameter. For example: Dubai OR Netherlands OR Belgium

- `description_filter` (string): Filter on the job description. You can search like you search on Google, see the documentation for more info.

- `advanced_description_filter` (string): Uses the same syntax as advanced_title_filter

- `organization_filter` (string): Filter on the job's company name. Only allows for exact matches. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:NVIDIA,Walmart Warning, this filter does not work for company names using parenthesis ( ) Please send us an email at remco@fantastic.jobs to receive a list of all companies in this API

- `organization_exclusion_filter` (string): Same syntax as the organization_filter. Filter out more than one company with a comma delimited list without spaces!. Requires an exact match. Use the advanced_organization_filter for more functionality

- `description_type` (string): Description Type. Leave empty to return data without job description. Option 1: 'text' Option 2: 'html'

- `remote` (string): Example value: 

- `source` (string): Filter on source. Your options are: adp, applicantpro, ashby, bamboohr, breezy, careerplug, comeet, csod, dayforce, eightfold, freshteam, gem, greenhouse, gohire, hirehive, hiringthing, icims, isolved, jazzhr, jobvite, join.com, kula, lever.co, oraclecloud, paycom, paylocity, personio, phenompeople, pinpoint, polymer, recruitee, recooty, smartrecruiters, successfactors, taleo, teamtailor, taleo, trakstar, workable, workday, zoho You can search on more than one sourcewith a comma delimited list w

- `source_exclusion` (string): Example value: 

- `advanced_organization_filter` (string): Advanced Organization filter which enables more features like parenthesis, 'AND', and prefix searching. This filter is also useful to exclude certain organizations. Phrases (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: University & ! Harvard Will ret

- `include_ai` (string): Example value: 

- `ai_employment_type_filter` (string): BETA Feature. Filter on a specific job type as identified by our AI, the options are: FULL_TIME/PART_TIME/CONTRACTOR/TEMPORARY/INTERN/VOLUNTEER/PER_DIEM/OTHER To filter on more than one job type, please delimit by comma, like such: FULL_TIME, PART_TIME

- `ai_work_arrangement_filter` (string): BETA Feature. Filter on a specific work arrangement identified by our AI, This is a more granular version of the 'remote' filter, which is quite broad. the options are: On-site (Job is on site only, no working from home available) Hybrid (Job is in the office with one or more days remote) Remote OK (Job is fully remote, but an office is available) Remote Solely (Job is fully remote, and no office is available) To filter on more than one job type, please delimit by comma with no space, like such:

- `ai_taxonomies_a_filter` (string): Example value: 

- `ai_taxonomies_a_primary_filter` (string): Filter the jobs on one or more top level primary taxonomies. This filter will filter on the primary taxonomy only (the first taxonomy in the array) You can filter on more than one taxonomy with a comma delimited list without spaces!. For example: ai_taxonomies_a_filter:Technology,Healthcare For taxonomies including &, please double-quote

- `ai_taxonomies_a_exclusion_filter` (string): Example value: 

- `ai_has_salary` (string): Example value: 

- `ai_experience_level_filter` (string): BETA Feature. Filter on a certain required experience level as identified by our AI, the options are: 0-2/2-5/5-10/10+ To filter on more than one job type, please delimit by comma with no space, like such: 0-2,2-5

- `ai_visa_sponsorship_filter` (string): Example value: 

- `include_li` (string): Example value: 

- `li_organization_slug_filter` (string): Filter on the job's company via the slug. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:netflix,walmart Only allows for exact matches, please check the exact company slug before filtering. The slug is the company specific part of the url. For example the slug in the following url is 'walmart': https://www.linkedin.com/company/walmart/ Please send us a message or email at remco@fantastic.jobs to receive a list of companies

- `li_organization_slug_exclusion_filter` (string): Similar to the slug filter, but it removes companies from the results.

- `li_industry_filter` (string): BETA Feature Filter on the organization's LinkedIn Industry. Please use the exact Industry name. This filter is case sensitive. You can filter on more than one industry with a comma-delimited list without spaces. For example: industry_filter=Accounting,Staffing and Recruiting If the industry contains a comma, please double-quote. You can find a list of industries on our website: https://fantastic.jobs/article/linkedin-industries

- `li_organization_specialties_filter` (string): BETA Feature Filter on the job's organization LinkedIn specialties, with the same syntax as our job search filters. Please note that not all companies have specialties listed on their company profile

- `li_organization_description_filter` (string): Filter on the company's description, with the same syntax as our job search filters

- `li_organization_employees_lte` (string): Use this to filter on jobs from companies less than a certain number of employees. Can be used in combination with li_organization_employees_gte. For example, if you wish to filter on small companies but want to exclude companies with just one employee, you can use the following query filter: employees_gte=1 employees_lte=200

- `ai_education_requirements_filter` (string): Example value: 



---


### `ultra____get_jobs_hourly`

Firehose API, includes jobs we discovered in the last hour. Perfect for one or more hourly API calls. Requires Ultra or Mega subscription

**端点**: `GET /active-ats-1h`


**参数**:

- `offset` (string): Offset allows you to paginate results. For example, if you want to retrieve 300 jobs from our api you can send 3 requests with offset 0, 100, and 200.

- `title_filter` (string): Search on the job title. You can search like you search on Google, see the documentation for more info.

- `advanced_title_filter` (string): Advanced Title filter which enables more features like parenthesis, 'AND', and prefix searching. Can Not be used in combination with regular title_filter Phrares (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: (AI | 'Machine Learning' | 'Robotics') & !

- `location_filter` (string): Filter on location. Please do not search on abbreviations like US, UK, NYC. Instead, search on full names like United States, New York, United Kingdom. You may filter on more than one location in a single API call using the OR parameter. For example: Dubai OR Netherlands OR Belgium

- `description_filter` (string): Filter on the job description. You can search like you search on Google, see the documentation for more info.

- `advanced_description_filter` (string): Uses the same syntax as advanced_title_filter

- `organization_filter` (string): Filter on the job's company name. Only allows for exact matches. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:NVIDIA,Walmart Warning, this filter does not work for company names using parenthesis ( ) Please send us an email at remco@fantastic.jobs to receive a list of all companies in this API

- `organization_exclusion_filter` (string): Same syntax as the organization_filter. Filter out more than one company with a comma delimited list without spaces!. Requires an exact match. Use the advanced_organization_filter for more functionality

- `description_type` (string): Description Type. Leave empty to return data without job description. Option 1: 'text' Option 2: 'html'

- `remote` (string): Example value: 

- `source` (string): You may optionally filter on the source, which are the ATS platforms. Your options are:adp, applicantpro, ashby, bamboohr, breezy, careerplug, comeet, csod, dayforce, eightfold, freshteam, gem, greenhouse, gohire, hirehive, hiringthing, icims, isolved, jazzhr, jobvite, join.com, kula, lever.co, oraclecloud, paycom, paylocity, personio, phenompeople, pinpoint, polymer, recruitee, recooty, smartrecruiters, successfactors, taleo, teamtailor, taleo, trakstar, workable, workday, zoho You can search o

- `source_exclusion` (string): You can exclude one or more sources with a comma delimited list without spaces!. For example: source_exclusion:workday,greenhouse

- `advanced_organization_filter` (string): Advanced Organization filter which enables more features like parenthesis, 'AND', and prefix searching. This filter is also useful to exclude certain organizations. Phrases (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: University & ! Harvard Will ret

- `include_ai` (string): Example value: 

- `ai_employment_type_filter` (string): BETA Feature. Filter on a specific job type as identified by our AI, the options are: FULL_TIME/PART_TIME/CONTRACTOR/TEMPORARY/INTERN/VOLUNTEER/PER_DIEM/OTHER To filter on more than one job type, please delimit by comma, like such: FULL_TIME, PART_TIME

- `ai_work_arrangement_filter` (string): BETA Feature. Filter on a specific work arrangement identified by our AI, This is a more granular version of the 'remote' filter, which is quite broad the options are: On-site (Job is on site only, no working from home available) Hybrid (Job is in the office with one or more days remote) Remote OK (Job is fully remote, but an office is available) Remote Solely (Job is fully remote, and no office is available) To filter on more than one job type, please delimit by comma with no space, like such: 

- `ai_taxonomies_a_filter` (string): Filter the jobs on one or more top level taxonomies. You can choose from: Technology, Healthcare, Management & Leadership, Finance & Accounting, Human Resources, Sales, Marketing, Customer Service & Support, Education, Legal, Engineering, Science & Research, Trades, Construction, Manufacturing, Logistics, Creative & Media, Hospitality, Environmental & Sustainability, Retail, Data & Analytics, Software, Energy, Agriculture, Social Services, Administrative, Government & Public Sector, Art & Design

- `ai_taxonomies_a_primary_filter` (string): Filter the jobs on one or more top level primary taxonomies. This filter will filter on the primary taxonomy only (the first taxonomy in the array) You can filter on more than one taxonomy with a comma delimited list without spaces!. For example: ai_taxonomies_a_filter:Technology,Healthcare For taxonomies including &, please double-quote

- `ai_taxonomies_a_exclusion_filter` (string): Use this parameter to exclude jobs with certain top level taxonomies from the results You can filter out more than one taxonomy with a comma delimited list without spaces!. For example: ai_taxonomies_a_exclusion_filter:Technology,Healthcare For taxonomies including &, please double-quote

- `ai_has_salary` (string): Example value: 

- `ai_experience_level_filter` (string): BETA Feature. Filter on a certain required experience level as identified by our AI, the options are: 0-2/2-5/5-10/10+ To filter on more than one job type, please delimit by comma with no space, like such: 0-2,2-5

- `ai_visa_sponsorship_filter` (string): Example value: 

- `include_li` (string): Example value: 

- `li_organization_slug_filter` (string): Filter on the job's company via the slug. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:netflix,walmart Only allows for exact matches, please check the exact company slug before filtering. The slug is the company specific part of the url. For example the slug in the following url is 'walmart': https://www.linkedin.com/company/walmart/ Please send us a message or email at remco@fantastic.jobs to receive a list of companies

- `li_organization_slug_exclusion_filter` (string): Similar to the slug filter, but it removes companies from the results.

- `li_industry_filter` (string): BETA Feature Filter on the organization's LinkedIn Industry. Please use the exact Industry name. This filter is case sensitive. You can filter on more than one industry with a comma-delimited list without spaces. For example: industry_filter=Accounting,Staffing and Recruiting If the industry contains a comma, please double-quote. You can find a list of industries on our website: https://fantastic.jobs/article/linkedin-industries

- `li_organization_specialties_filter` (string): BETA Feature Filter on the job's organization LinkedIn specialties, with the same syntax as our job search filters. Please note that not all companies have specialties listed on their company profile

- `li_organization_description_filter` (string): Filter on the company's description, with the same syntax as our job search filters

- `li_organization_employees_lte` (string): Use this to filter on jobs from companies less than a certain number of employees. Can be used in combination with li_organization_employees_gte. For example, if you wish to filter on small companies but want to exclude companies with just one employee, you can use the following query filter: employees_gte=1 employees_lte=200

- `li_organization_employees_gte` (string): Use this to filter on jobs from companies greater than a certain number of employees. Can be used in combination with li_organization_employees_lte. For example, if you wish to filter on small companies but want to exclude companies with just one employee, you can use the following query filter: employees_gte=1 employees_lte=200

- `ai_education_requirements_filter` (string): Please contact us before using



---


### `ultra___get_jobs_backfill___6m`

You can use this endpoint to backfill your job application before moving on to the 7d, 24h, or hourly endpoint

**端点**: `GET /active-ats-6m`


**参数**:

- `limit` (string): Warning, this endpoint is for backfill purposes and goes up to 500 jobs per API call. These jobs count towards your job credits You can limit the number of jobs per API call between 10 and 500. If left blank, the default value is 500 Use the offset parameter to receive the next batch of jobs

- `offset` (string): Offset allows you to paginate results. For example, if you want to retrieve 1500 jobs from our api you can send 3 requests with limit=500 and offset= 0, 500, and 1000.

- `title_filter` (string): Search on the job title. You can search like you search on Google, see the documentation for more info.

- `advanced_title_filter` (string): Advanced Title filter which enables more features like parenthesis, 'AND', and prefix searching. Can Not be used in combination with regular title_filter Phrares (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: (AI | 'Machine Learning' | 'Robotics') & !

- `location_filter` (string): Filter on location. Please do not search on abbreviations like US, UK, NYC. Instead, search on full names like United States, New York, United Kingdom. You may filter on more than one location in a single API call using the OR parameter. For example: Dubai OR Netherlands OR Belgium

- `description_filter` (string): Filter on the job description. You can search like you search on Google, see the documentation for more info. Warning, for the 6 month endpoint, only use the description filter for very specific searches, or to narrow down after having applied other filters. There's a risk of timeouts when searching on very common words and sentences. Be as specific as possible when using description_filter.

- `advanced_description_filter` (string): Uses the same syntax as advanced_title_filter Warning, for the 6 month endpoint, only use the description filter for very specific searches, or to narrow down after having applied other filters. There's a risk of timeouts when searching on very common words and sentences. Be as specific as possible when using description_filter.

- `organization_filter` (string): Filter on the job's company name. Only allows for exact matches. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:NVIDIA,Walmart Warning, this filter does not work for company names using parenthesis ( ) Please send us an email at remco@fantastic.jobs to receive a list of all companies in this API

- `organization_exclusion_filter` (string): Same syntax as the organization_filter. Filter out more than one company with a comma delimited list without spaces!. Requires an exact match. Use the advanced_organization_filter for more functionality

- `description_type` (string): Description Type. Leave empty to return data without job description. Option 1: 'text' Option 2: 'html'

- `remote` (string): Example value: 

- `source` (string): You may optionally filter on the source, which are the ATS platforms. Your options are:adp, applicantpro, ashby, bamboohr, breezy, careerplug, comeet, csod, dayforce, eightfold, freshteam, gem, greenhouse, gohire, hirehive, hiringthing, icims, isolved, jazzhr, jobvite, join.com, kula, lever.co, oraclecloud, paycom, paylocity, personio, phenompeople, pinpoint, polymer, recruitee, recooty, smartrecruiters, successfactors, taleo, teamtailor, taleo, trakstar, workable, workday, zoho You can search o

- `source_exclusion` (string): You can exclude one or more sources with a comma delimited list without spaces!. For example: source_exclusion:workday,greenhouse

- `advanced_organization_filter` (string): Advanced Organization filter which enables more features like parenthesis, 'AND', and prefix searching. This filter is also useful to exclude certain organizations. Phrases (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: University & ! Harvard Will ret

- `include_ai` (string): Example value: 

- `ai_employment_type_filter` (string): BETA Feature. Filter on a specific job type as identified by our AI, the options are: FULL_TIME/PART_TIME/CONTRACTOR/TEMPORARY/INTERN/VOLUNTEER/PER_DIEM/OTHER To filter on more than one job type, please delimit by comma, like such: FULL_TIME, PART_TIME

- `ai_work_arrangement_filter` (string): BETA Feature. Filter on a specific work arrangement identified by our AI, This is a more granular version of the 'remote' filter, which is quite broad. the options are: On-site (Job is on site only, no working from home available) Hybrid (Job is in the office with one or more days remote) Remote OK (Job is fully remote, but an office is available) Remote Solely (Job is fully remote, and no office is available) To filter on more than one job type, please delimit by comma with no space, like such:

- `ai_has_salary` (string): Example value: 

- `ai_taxonomies_a_filter` (string): Filter the jobs on one or more top level taxonomies. You can choose from: Technology, Healthcare, Management & Leadership, Finance & Accounting, Human Resources, Sales, Marketing, Customer Service & Support, Education, Legal, Engineering, Science & Research, Trades, Construction, Manufacturing, Logistics, Creative & Media, Hospitality, Environmental & Sustainability, Retail, Data & Analytics, Software, Energy, Agriculture, Social Services, Administrative, Government & Public Sector, Art & Design

- `ai_taxonomies_a_primary_filter` (string): Filter the jobs on one or more top level primary taxonomies. This filter will filter on the primary taxonomy only (the first taxonomy in the array) You can filter on more than one taxonomy with a comma delimited list without spaces!. For example: ai_taxonomies_a_filter:Technology,Healthcare For taxonomies including &, please double-quote

- `ai_taxonomies_a_exclusion_filter` (string): Use this parameter to exclude jobs with certain top level taxonomies from the results You can filter out more than one taxonomy with a comma delimited list without spaces!. For example: ai_taxonomies_a_exclusion_filter:Technology,Healthcare For taxonomies including &, please double-quote

- `ai_experience_level_filter` (string): BETA Feature. Filter on a certain required experience level as identified by our AI, the options are: 0-2/2-5/5-10/10+ To filter on more than one job type, please delimit by comma with no space, like such: 0-2,2-5

- `ai_visa_sponsorship_filter` (string): Example value: 

- `include_li` (string): Example value: 

- `li_organization_slug_filter` (string): Filter on the job's company via the slug. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:netflix,walmart Only allows for exact matches, please check the exact company slug before filtering. The slug is the company specific part of the url. For example the slug in the following url is 'walmart': https://www.linkedin.com/company/walmart/ Please send us a message or email at remco@fantastic.jobs to receive a list of companies

- `li_organization_slug_exclusion_filter` (string): Similar to the slug filter, but it removes companies from the results.

- `li_industry_filter` (string): BETA Feature Filter on the organization's LinkedIn Industry. Please use the exact Industry name. This filter is case sensitive. You can filter on more than one industry with a comma-delimited list without spaces. For example: industry_filter=Accounting,Staffing and Recruiting If the industry contains a comma, please double-quote. You can find a list of industries on our website: https://fantastic.jobs/article/linkedin-industries

- `li_organization_specialties_filter` (string): BETA Feature Filter on the job's organization LinkedIn specialties, with the same syntax as our job search filters. Please note that not all companies have specialties listed on their company profile

- `li_organization_description_filter` (string): Filter on the company's description, with the same syntax as our job search filters

- `li_organization_employees_lte` (string): Use this to filter on jobs from companies less than a certain number of employees. Can be used in combination with li_organization_employees_gte. For example, if you wish to filter on small companies but want to exclude companies with just one employee, you can use the following query filter: employees_gte=1 employees_lte=200



---


### `get_jobs_24h`

Search and retrieve jobs on title, description, location, remote, and organization. Optionally add a text or html description. The jobs in this API have been indexed by us during the last 24 hours.

**端点**: `GET /active-ats-24h`


**参数**:

- `limit` (string): You can limit the number of jobs per API call between 10 and 100. If left blank, the default value is 100 Use the offset parameter to receive the next batch of jobs

- `offset` (string): Offset allows you to paginate results. For example, if you want to retrieve 300 jobs from our api you can send 3 requests with limit=100 and offset= 0, 100, and 200. With a limit of 10, you can fetch 30 jobs using 3 requests with offset= 0, 10, and 20

- `title_filter` (string): Search on the job title. You can search like you search on Google, see the documentation for more info.

- `advanced_title_filter` (string): Advanced Title filter which enables more features like parenthesis, 'AND', and prefix searching. Can Not be used in combination with regular title_filter Phrares (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: (AI | 'Machine Learning' | 'Robotics') & !

- `location_filter` (string): Filter on location. Please do not search on abbreviations like US, UK, NYC. Instead, search on full names like United States, New York, United Kingdom. You may filter on more than one location in a single API call using the OR parameter. For example: Dubai OR Netherlands OR Belgium

- `description_filter` (string): Filter on the job description. You can search like you search on Google, see the documentation for more info.

- `advanced_description_filter` (string): Uses the same syntax as advanced_title_filter

- `organization_filter` (string): Filter on the job's company name. Only allows for exact matches. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:NVIDIA,Walmart Warning, this filter does not work for company names using parenthesis ( ) Please send us an email at remco@fantastic.jobs to receive a list of all companies in this API

- `organization_exclusion_filter` (string): Same syntax as the organization_filter. Filter out more than one company with a comma delimited list without spaces!. Requires an exact match. Use the advanced_organization_filter for more functionality

- `description_type` (string): Description Type. Leave empty to return data without job description. Option 1: 'text' Option 2: 'html'

- `remote` (string): Example value: 

- `source` (string): You may optionally filter on the source, which are the ATS platforms. Your options are:adp, applicantpro, ashby, bamboohr, breezy, careerplug, comeet, csod, dayforce, eightfold, freshteam, gem, greenhouse, gohire, hirehive, hiringthing, icims, isolved, jazzhr, jobvite, join.com, kula, lever.co, oraclecloud, paycom, paylocity, personio, phenompeople, pinpoint, polymer, recruitee, recooty, smartrecruiters, successfactors, taleo, teamtailor, taleo, trakstar, workable, workday, zoho You can search o

- `source_exclusion` (string): You can exclude one or more sources with a comma delimited list without spaces!. For example: source_exclusion:workday,greenhouse

- `date_filter` (string): ou can use this filter to return only the most recent jobs, instead of all jobs from the last 7 days. This filter is a greater than filter. For example, if today's date is 2025-01-03 and you wish to only return jobs posted in 2025, you can filter on '2025-01-01'. To include time, use the following syntax: '2025-01-01T14:00:00' Please keep in mind that the jobs posted date/time is UTC and there's a 1 to 2 hour delay before jobs appear on this API.

- `advanced_organization_filter` (string): Advanced Organization filter which enables more features like parenthesis, 'AND', and prefix searching. This filter is also useful to exclude certain organizations. Phrases (two words or more) always need to be single quoted or use the operator <-> Instead of using natural language like 'OR' you need to use operators like: & (AND) | (OR) ! (NOT) <-> (FOLLOWED BY) ' ' (FOLLOWED BY alternative, does not work with 6. Prefix Wildcard) :* (Prefix Wildcard) For example: University & ! Harvard Will ret

- `include_ai` (string): Example value: 

- `ai_employment_type_filter` (string): BETA Feature. Filter on a specific job type as identified by our AI, the options are: FULL_TIME/PART_TIME/CONTRACTOR/TEMPORARY/INTERN/VOLUNTEER/PER_DIEM/OTHER To filter on more than one job type, please delimit by comma, like such: FULL_TIME, PART_TIME

- `ai_work_arrangement_filter` (string): BETA Feature. Filter on a specific work arrangement identified by our AI, This is a more granular version of the 'remote' filter, which is quite broad. the options are: On-site (Job is on site only, no working from home available) Hybrid (Job is in the office with one or more days remote) Remote OK (Job is fully remote, but an office is available) Remote Solely (Job is fully remote, and no office is available) To filter on more than one job type, please delimit by comma with no space, like such:

- `ai_taxonomies_a_filter` (string): Filter the jobs on one or more top level taxonomies. You can choose from: Technology, Healthcare, Management & Leadership, Finance & Accounting, Human Resources, Sales, Marketing, Customer Service & Support, Education, Legal, Engineering, Science & Research, Trades, Construction, Manufacturing, Logistics, Creative & Media, Hospitality, Environmental & Sustainability, Retail, Data & Analytics, Software, Energy, Agriculture, Social Services, Administrative, Government & Public Sector, Art & Design

- `ai_taxonomies_a_primary_filter` (string): Filter the jobs on one or more top level primary taxonomies. This filter will filter on the primary taxonomy only (the first taxonomy in the array) You can filter on more than one taxonomy with a comma delimited list without spaces!. For example: ai_taxonomies_a_filter:Technology,Healthcare For taxonomies including &, please double-quote

- `ai_taxonomies_a_exclusion_filter` (string): Use this parameter to exclude jobs with certain top level taxonomies from the results You can filter out more than one taxonomy with a comma delimited list without spaces!. For example: ai_taxonomies_a_exclusion_filter:Technology,Healthcare For taxonomies including &, please double-quote

- `ai_has_salary` (string): Example value: 

- `ai_experience_level_filter` (string): BETA Feature. Filter on a certain required experience level as identified by our AI, the options are: 0-2/2-5/5-10/10+ To filter on more than one job type, please delimit by comma with no space, like such: 0-2,2-5

- `ai_visa_sponsorship_filter` (string): Example value: 

- `include_li` (string): Example value: 

- `li_organization_slug_filter` (string): Filter on the job's company via the slug. You can search on more than one company with a comma delimited list without spaces!. For example: organization_filter:netflix,walmart Only allows for exact matches, please check the exact company slug before filtering. The slug is the company specific part of the url. For example the slug in the following url is 'walmart': https://www.linkedin.com/company/walmart/ Please send us a message or email at remco@fantastic.jobs to receive a list of companies

- `li_organization_slug_exclusion_filter` (string): Similar to the slug filter, but it removes companies from the results.

- `li_industry_filter` (string): BETA Feature Filter on the organization's LinkedIn Industry. Please use the exact Industry name. This filter is case sensitive. You can filter on more than one industry with a comma-delimited list without spaces. For example: industry_filter=Accounting,Staffing and Recruiting If the industry contains a comma, please double-quote. You can find a list of industries on our website: https://fantastic.jobs/article/linkedin-industries

- `li_organization_specialties_filter` (string): BETA Feature Filter on the job's organization LinkedIn specialties, with the same syntax as our job search filters. Please note that not all companies have specialties listed on their company profile

- `li_organization_description_filter` (string): Filter on the company's description, with the same syntax as our job search filters

- `li_organization_employees_lte` (string): Use this to filter on jobs from companies less than a certain number of employees. Can be used in combination with li_organization_employees_gte. For example, if you wish to filter on small companies but want to exclude companies with just one employee, you can use the following query filter: employees_gte=1 employees_lte=200

- `li_organization_employees_gte` (string): Use this to filter on jobs from companies less than a certain number of employees. Can be used in combination with li_organization_employees_gte. For example, if you wish to filter on small companies but want to exclude companies with just one employee, you can use the following query filter: employees_gte=1 employees_lte=200

- `ai_education_requirements_filter` (string): Please contact us before using



---


### `ultra___get_expired_jobs`

Contains IDs of jobs that were flagged as expired yesterday. Updates once per day at 01:30 UTC. Requires Ultra or Mega subscription

**端点**: `GET /active-ats-expired`



---



## 技术栈

- **传输协议**: stdio
- **HTTP 客户端**: httpx

## 开发

此服务器由 [API-to-MCP](https://github.com/BACH-AI-Tools/api-to-mcp) 工具自动生成。

版本: 1.0.0
