---
title: "For Loop Vs lapply"
date: 2021-09-30T17:06:05+07:00
categories: [tutorial]
tags: [rstats]
---

**TL;DR**

> Saya ingin membandingkan dua kode dalam bahasa R yang saya susun sedemikian rupa sehingga menghasilkan objek yang sama. Kasus: data lowongan kerja.

{{< toc >}}

## Pustaka R

Pada tes ini, dibutuhkan beberapa package di antaranya:

```R
lapply(
  c(
    "httr",
    "jsonlite",
    "stringr",
    "dplyr",
    "tidyr",
    "janitor",
    "waldo",
    "microbenchmark"
  ), function(x) if(!require(x, character.only = TRUE)) install.packages(x)
)
```

Juga sebuah fungsi yang ditulis oleh abang-abang Jerman bernama-akun rentrop seperti yang [ada di sini](https://gist.github.com/rentrop/83cb1d8fc8593726a808032e55314019). Fungsi tersebut memanfaatkan pustaka **httr** dan **jsonlite** untuk berinteraksi dengan data menggunakan API untuk basisdata GraphQL. Saya simpan sebagai berkas skrip R dengan nama "function_graphql.R" dan memanggilnya dengan `source()` dari konsol R. 

```R
source("function_graphql.R")
```

## Parameter dan Query

Contoh data yang digunakan merupakan data lowongan pekerjaan dari Jobstreet. Ada beberapa parameter yang dibutuhkan, di antaranya tentu saja ada URL ke API-nya yang pada kasus ini saya simpan dalam variabel `url`. Kemudian karena yang saya lakukan sama seperti ketika kita mencari lowongan melalui antar muka web menggunakan suatu kata kunci, maka perlu ada `key` untuk menyaring lowongan pekerjaan yang sesuai. Berikutnya variabel `page` juga diperlukan karena ini sama dengan kita mencari lowongan kerja di web, ada halaman-halaman yang perlu dilalui.

```R
url <- "https://xapi.supercharge-srp.co/job-search/graphql?country=id&isSmartSearch=true"
key <- "data analyst"
page <- 1
```

Selain itu untuk mengakses basis data GraphQL khususnya akses basis data milik Jobstreet di URL tersebut, dibutuhkan beberapa parameter lain yakni variabel pencarian guna memfilter hasil dan tentu saya query-nya. Untuk variabel pencarian saya simpan pada objek atau variabel `var` seperti berikut:

```R
var <- sprintf(
  '{
    "keyword": "%s",
    "jobFunctions": [
      501,
      503,
      508,
      512
    ],
    "locations": [],
    "salaryType": 1,
    "jobTypes": [],
    "createdAt": null,
    "careerLevels": [],
    "page": %s,
    "country": "id",
    "sVi": "",
    "categories": [
      "501",
      "503",
      "508",
      "512"
    ],
    "workTypes": [],
    "industries": [],
    "locale": "id"
  }', key, page
)
```

Sementara itu query yang digunakan lumayan panjang juga, seperti berikut:

```R
query <- 
  'query getJobs($country: String, $locale: String, $keyword: String, $createdAt: String, $jobFunctions: [Int], $categories: [String], $locations: [Int], $careerLevels: [Int], $minSalary: Int, $maxSalary: Int, $salaryType: Int, $candidateSalary: Int, $candidateSalaryCurrency: String, $datePosted: Int, $jobTypes: [Int], $workTypes: [String], $industries: [Int], $page: Int, $pageSize: Int, $companyId: String, $advertiserId: String, $userAgent: String, $accNums: Int, $subAccount: Int, $minEdu: Int, $maxEdu: Int, $edus: [Int], $minExp: Int, $maxExp: Int, $seo: String, $searchFields: String, $candidateId: ID, $isDesktop: Boolean, $isCompanySearch: Boolean, $sort: String, $sVi: String, $duplicates: String, $flight: String, $solVisitorId: String) {
  jobs(country: $country, locale: $locale, keyword: $keyword, createdAt: $createdAt, jobFunctions: $jobFunctions, categories: $categories, locations: $locations, careerLevels: $careerLevels, minSalary: $minSalary, maxSalary: $maxSalary, salaryType: $salaryType, candidateSalary: $candidateSalary, candidateSalaryCurrency: $candidateSalaryCurrency, datePosted: $datePosted, jobTypes: $jobTypes, workTypes: $workTypes, industries: $industries, page: $page, pageSize: $pageSize, companyId: $companyId, advertiserId: $advertiserId, userAgent: $userAgent, accNums: $accNums, subAccount: $subAccount, minEdu: $minEdu, edus: $edus, maxEdu: $maxEdu, minExp: $minExp, maxExp: $maxExp, seo: $seo, searchFields: $searchFields, candidateId: $candidateId, isDesktop: $isDesktop, isCompanySearch: $isCompanySearch, sort: $sort, sVi: $sVi, duplicates: $duplicates, flight: $flight, solVisitorId: $solVisitorId) {
    ...LegacyCompat_SearchResult
  }
}

fragment LegacyCompat_SearchResult on SearchResult {
  solMetadata
  jobs {
    id
    sourceCountryCode
    isStandout
    companyMeta {
      id
      isPrivate
      name
    }
    jobTitle
    jobUrl
    jobTitleSlug
    description
    employmentTypes {
      name
    }
    sellingPoints
    locations {
      code
      name
      children {
        code
        name
      }
    }
    categories {
      code
      name
      children {
        code
        name
      }
    }
    postedAt
    salaryRange {
      currency
      max
      min
      period
      term
    }
    isClassified
  }
}'
```

Sebetulnya saya juga kurang begitu paham dan masih mempelajari salah satu *graph database* ini. Untuk query yang panjang ini saya copas dari hasil *inspect element* di peramban yang saya gunakan. Penjelasan tentang URL-based query untuk GraphQL mungkin bisa dipelajari pada [laman berikut](https://blog.logrocket.com/designing-url-based-query-syntax-graphql/).

## Mengambil Data

Tiba saatnya untuk coba menarik (*pulling*) data. Tidak berjalan lama karena hanya sekitar 30 rekaman di halaman pertama saja. Di sinilah fungsi `GQL()` dari Abang rentrop menjadi sangat bermanfaat.

```R
jobs <- GQL(
  query = query,
  .variables = var,
  .url = url
)

job <- jobs$jobs$jobs
str(job[[1]])
```

Akan dihasilkan objek dengan struktur list. Saya definisikan dalam `job` saja. Setelah subset konten yang dibutuhkan saja menjadi objek `job`, kita bisa amati strukturnya menjadi seperti berikut ini (hanya item pertama dari 30 sebagai sampel, karena tentu saja strukturnya akan berulang):

```
List of 15
 $ id               : chr "3641190"
 $ sourceCountryCode: chr "id"
 $ isStandout       : logi TRUE
 $ companyMeta      :List of 3
  ..$ id       : chr "433563"
  ..$ isPrivate: logi FALSE
  ..$ name     : chr "PT Indoglobal Nusa Persada"
 $ jobTitle         : chr "SYSTEM ANALYST"
 $ jobUrl           : chr "https://www.jobstreet.co.id/id/job/system-analyst-3641190?token=0~1daa0355-a242-4f92-87a9-90dbbca3a275&sectionR"| __truncated__
 $ jobTitleSlug     : chr "system-analyst"
 $ description      : chr "Design new IT solutions, modify, enhance or adapt existing systems and integrate new features or improvements i"| __truncated__
 $ employmentTypes  :List of 1
  ..$ :List of 1
  .. ..$ name: chr "Penuh Waktu"
 $ sellingPoints    :List of 3
  ..$ : chr "Good reputation company at the national level as edutech platform"
  ..$ : chr "Incentive / Rewards Project"
  ..$ : chr "A great environment, culture and partner"
 $ locations        :List of 1
  ..$ :List of 3
  .. ..$ code    : chr "30500"
  .. ..$ name    : chr "Jakarta Raya"
  .. ..$ children: NULL
 $ categories       :List of 2
  ..$ :List of 3
  .. ..$ code    : chr "508"
  .. ..$ name    : chr "Komputer/Teknologi Informasi"
  .. ..$ children: NULL
  ..$ :List of 3
  .. ..$ code    : chr "191"
  .. ..$ name    : chr "IT-Perangkat Lunak"
  .. ..$ children: NULL
 $ postedAt         : chr "2021-09-28T05:34:48Z"
 $ salaryRange      :List of 5
  ..$ currency: NULL
  ..$ max     : NULL
  ..$ min     : NULL
  ..$ period  : chr "monthly"
  ..$ term    : NULL
 $ isClassified     : logi FALSE
```

Selain menghasilkan kumpulan data lowongan, fungsi `GQL()` dengan query dan parameter lain di atas juga menyimpan keterangan mengenai sesi yang terjadi ketika pengambilan data berlangsung, terdapat pada:

```R
(query_meta <- jobs$jobs$solMetadata)
```

## Perbandingan Skrip

### Kode pertama dengan `lapply()`

Untuk skrip pertama saya memanfaatkan fungsi `lapply()` yang disediakan oleh pustaka bawaan R yakni base. Agar dapat dibandingkan dengan mudah nantinya saya buat jadi fungsi `v1()` saja.

```R
# method 1
v1 <- function(job){
  
  vacancy <- lapply(job, function(x){
    v <- unlist(x)
    v <- data.frame(name = names(v), value = v)
    v <- as_tibble(v)
    v <- v %>% 
      group_by(name) %>% 
      summarise_all(~toString(value)) %>% 
      ungroup()
    return(v)
  })
  
  vacancy <- lapply(vacancy, function(x){
    v <- x %>% 
      pivot_wider(
        names_from = "name",
        values_from = "value"
      )
    v <- janitor::clean_names(v)
    return(v)
  })
  
  v1 <- do.call("bind_rows", vacancy)
  return(v1)
  
}

vacancy1 <- v1(job)
```

Konten datanya dibahas di akhir saja, ya... Kali ini fokus pada perbandingan dua skrip yang saya susun dulu. 

### Kode kedua dengan `for` loop

Untuk skrip kedua, saya gunakan `for` loop, yakni salah satu metode dasar pada tiap bahasa pemrograman untuk mengiterasi proses pada sequencial vector atau list.

Setelah itu, dilanjutkan dengan menggunakan fungsi-fungsi dari pustaka **dplyr** dan **tidyr**, juga meminjam fungsi `clean_names()` dari **janitor** untuk hidup lebih mudah. Skrip ini hanya mereplikasi fungsi-fungsi yang berjalan dengan skrip sebelumnya, tentunya dengan penyesuaian karena struktur objek yang diproses jadi berbeda.

```R
# method 2
v2 <- function(job){
  
  for (i in seq_along(job)) {
    s <- unlist(job[[i]])
    s <- cbind(name = names(s), value = s)
    s <- as_tibble(s) %>% mutate(num = i)
    if(i == 1){
      vacancy <- s
    } else {
      vacancy <- bind_rows(vacancy, s)
    }
  }
  
  v2 <- vacancy %>% 
    group_by(num, name) %>%
    summarise_all(~toString(value)) %>% 
    ungroup() %>% 
    pivot_wider(
      id_cols = "num", 
      names_from = "name",
      values_from = "value"
    ) %>% 
    select(-num)
  
  v2 <- janitor::clean_names(v2)
  return(v2)
  
}

vacancy2 <- v2(job)
```

### Perbandingan

Kedua skrip atau fungsi di atas dibuat agar hasil keluarannya pun menjadi identik. Untuk memeriksanya saya menggunakan fungsi `waldo::compare()` seperti berikut.

```R
waldo::compare(vacancy1, vacancy2, x_arg = "v1", y_arg = "v2")
```

Menghasilkan keterangan bahwa kedua objek `v1` dan `v2` tidak memiliki perbedaan: ✓ No differences

Kemudian tiba saatnya pada bagian inti, yaitu perbandingan kedua metode di atas, saya menggunakan bantuan dari pustaka **microbenchmark** dan menyimpan hasilnya dalam variabel `b` agar mudah dieksplorasi nantinya.

```R
b <- microbenchmark::microbenchmark(v1(job), v2(job))
```

Menghasilkan keluaran seperti berikut:

```
Unit: milliseconds
    expr      min       lq      mean    median        uq       max neval
 v1(job) 940.4223 999.8946 1068.7362 1025.7667 1123.6142 1444.3575   100
 v2(job) 162.2252 171.1944  186.4427  178.5282  189.2315  343.9679   100
```

Terjadi 100 kali pengulangan `neval` untuk masing-masing expression (`expr`), n-evaluation, katakanlah begitu. Parameter default fungsi tersebut memang mengulang operasi sebanyak 100 kali. Untuk jumlah lainnya bisa menggunakan argumen `times`. Dapat pula membandingkan hasil dengan boxplot. Berikut statistik untuk 300 kali pengulangan.

```R
b2 <- microbenchmark::microbenchmark(v1(job), v2(job), times = 300L)
boxplot(b2, log = FALSE, horizontal = TRUE, ylab = "Time (millisecond)")
```

![benchmark](https://telegra.ph/file/663ca9a54fc2f589f27b4.png)

Dengan for loop sekali di awal dan diikuti dengan **dplyr** + **tidyr** tampak lebih konsisten kecepatannya dan lebih baik performanya.

## Merapikan Data

Setelah mengetahui baris kode mana yang baik, itulah yang saya simpan sebagai fungsi yang nantinya akan memudahkan jika ingin mengambil data lowongan kerja dari Jobstreet lewat R. Mari kita rapikan sedikit data yang sudah kita kumpulkan.

```R
vacancy <- vacancy2 %>% 
  select(
    id, matches("job"), posted_at, matches("categories"),
    description, matches("company"), matches("employ"),
    matches("is_"), matches("location"), matches("country"), 
    matches("salary"), matches("selling")
  ) %>% 
  select(-job_title_slug)
vacancy
```

Hasilnya kurang lebih seperti ini dalam format data.frame kelas **tibble**:

```
# A tibble: 30 × 23
   id      job_title job_url posted_at categories_code categories_name description
   <chr>   <chr>     <chr>   <chr>     <chr>           <chr>           <chr>      
 1 3641190 SYSTEM A… https:… 2021-09-… 508, 191        Komputer/Tekno… Design new…
 2 3643310 IT Progr… https:… 2021-09-… 508, 191        Komputer/Tekno… RESPONSIBI…
 3 3644140 Data Ana… https:… 2021-09-… 512, 103        Sains, Aktuari… Requiremen…
 4 3643734 Data Ana… https:… 2021-09-… 503, 203        Penjualan / Pe… Requiremen…
 5 3644293 Sales Da… https:… 2021-09-… 508, 193        Komputer/Tekno… Tanggung J…
 6 3644446 Sales Da… https:… 2021-09-… 512, 103        Sains, Aktuari… Responsibi…
 7 3644353 Digital … https:… 2021-09-… 503, 203        Penjualan / Pe… Job Descri…
 8 3632503 Data Sci… https:… 2021-09-… 508, 191        Komputer/Tekno… You will b…
 9 3644514 Data Sci… https:… 2021-09-… 508, 191        Komputer/Tekno… Requiremen…
10 3642934 Speciali… https:… 2021-09-… 508, 193        Komputer/Tekno… Responsibi…
# … with 20 more rows, and 16 more variables: company_meta_id <chr>,
#   company_meta_is_private <chr>, company_meta_name <chr>,
#   employment_types_name <chr>, is_classified <chr>, is_standout <chr>,
#   locations_code <chr>, locations_name <chr>, source_country_code <chr>,
#   salary_range_period <chr>, salary_range_currency <chr>,
#   salary_range_max <chr>, salary_range_min <chr>, selling_points1 <chr>,
#   selling_points2 <chr>, selling_points3 <chr>
```

## Session Info

```R
sessionInfo()
```

```
R version 4.0.4 (2021-02-15)
Platform: x86_64-pc-linux-gnu (64-bit)
Running under: Ubuntu 20.04.3 LTS

Matrix products: default
BLAS:   /usr/lib/x86_64-linux-gnu/blas/libblas.so.3.9.0
LAPACK: /usr/lib/x86_64-linux-gnu/lapack/liblapack.so.3.9.0

locale:
 [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
 [3] LC_TIME=id_ID.UTF-8        LC_COLLATE=en_US.UTF-8    
 [5] LC_MONETARY=id_ID.UTF-8    LC_MESSAGES=en_US.UTF-8   
 [7] LC_PAPER=id_ID.UTF-8       LC_NAME=C                 
 [9] LC_ADDRESS=C               LC_TELEPHONE=C            
[11] LC_MEASUREMENT=id_ID.UTF-8 LC_IDENTIFICATION=C       

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
[1] jsonlite_1.7.2 janitor_2.1.0  tidyr_1.1.3    dplyr_1.0.7    stringr_1.4.0 
[6] httr_1.4.2    

loaded via a namespace (and not attached):
 [1] Rcpp_1.0.7           rstudioapi_0.13      magrittr_2.0.1      
 [4] tidyselect_1.1.1     R6_2.5.0             rlang_0.4.11        
 [7] fansi_0.5.0          tools_4.0.4          waldo_0.3.0         
[10] utf8_1.2.1           cli_3.0.1            DBI_1.1.1           
[13] ellipsis_0.3.2       assertthat_0.2.1     tibble_3.1.4        
[16] lifecycle_1.0.0      crayon_1.4.1         purrr_0.3.4         
[19] microbenchmark_1.4-7 vctrs_0.3.8          curl_4.3.2          
[22] snakecase_0.11.0     glue_1.4.2           stringi_1.7.3       
[25] compiler_4.0.4       pillar_1.6.2         generics_0.1.0      
[28] lubridate_1.7.10     pkgconfig_2.0.3
```

Sekian dan terima kasih.
