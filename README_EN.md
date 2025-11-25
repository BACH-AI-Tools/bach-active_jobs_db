# Active Jobs Db MCP Server

English | [简体中文](./README.md) | [繁體中文](./README_ZH-TW.md)

## 🚀 Quick Start with EMCP Platform

**[EMCP](https://sit-emcp.kaleido.guru)** is a powerful MCP server management platform that allows you to quickly use various MCP servers without manual configuration!

### Quick Start:

1. 🌐 Visit **[EMCP Platform](https://sit-emcp.kaleido.guru)**
2. 📝 Register and login
3. 🎯 Go to **MCP Marketplace** to browse all available MCP servers
4. 🔍 Search or find this server (`bach-active_jobs_db`)
5. 🎉 Click the **"Install MCP"** button
6. ✅ Done! You can now use it in your applications

### EMCP Platform Advantages:

- ✨ **Zero Configuration**: No need to manually edit config files
- 🎨 **Visual Management**: Easy-to-use GUI for managing all MCP servers
- 🔐 **Secure & Reliable**: Centralized API key and authentication management
- 🚀 **One-Click Install**: Rich selection of servers in MCP Marketplace
- 📊 **Usage Statistics**: Real-time service call monitoring

Visit **[EMCP Platform](https://sit-emcp.kaleido.guru)** now to start your MCP journey!


---

## Introduction

This is an automatically generated MCP server using [FastMCP](https://fastmcp.wiki) for accessing the Active Jobs Db API.

- **PyPI Package**: `bach-active_jobs_db`
- **Version**: 1.0.0
- **Transport Protocol**: stdio


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

## Configuration

### API Authentication

This API requires authentication. Please set environment variable:

```bash
export API_KEY="your_api_key_here"
```

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `API_KEY` | API Key | Yes |
| `PORT` | N/A | No |
| `HOST` | N/A | No |



### 在 Claude Desktop 中使用

编辑 Claude Desktop 配置文件 `claude_desktop_config.json`:


```json
{
  "mcpServers": {
    "active_jobs_db": {
      "command": "python",
      "args": ["E:\path\to\active_jobs_db\server.py"],
      "env": {
        "API_KEY": "your_api_key_here"
      }
    }
  }
}
```

**Note**: Replace `E:\path\to\active_jobs_db\server.py` with the actual server file path.


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

- **FastMCP**: 快速、Pythonic 的 MCP 服务器框架
- **传输协议**: stdio
- **HTTP 客户端**: httpx

## 开发

This server is automatically generated by [API-to-MCP](https://github.com/BACH-AI-Tools/api-to-mcp) tool.

Version: 1.0.0
