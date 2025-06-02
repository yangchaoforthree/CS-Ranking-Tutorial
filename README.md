# CS Ranking Tutorial

This tutorial is to help you better understand how CS ranking works and how to correctly record professor/faculty information.

## 1. How to Record Valid Faculty Information for Your Institution's CS Ranking 
**Step-0**: Read the [official website](https://csrankings.org/#/index?all&us) first.

**Step-1**: Fork the official [CS rankings repository](https://github.com/emeryberger/CSrankings) and clone your forked copy locally.

**Step-2**: Read [CONTRIBUTING.md](https://github.com/emeryberger/CSrankings/blob/gh-pages/CONTRIBUTING.md) carefully. You only need to modify csrankings-[a-z].csv and counrtry-info.csv to contain the professor/faculty information and institution information of the corresponding first letter.

**Step-3**: Notes on modification
- Don't use EXCEL to modify the csv files, use editor like Notepad.
- Do not add a space after the comma.
- When adding information to csrankings-[a-z].csv, add it in alphabetical order, not at the end. You can use a script to sort and rewrite each line of text after adding it.
- If there are multiple entries for professor/faculty information on the dblp website, you need to add the corresponding number. (If you are not sure, the official recommendation is to contact dblp, or you can contact the corresponding professor/faculty to complete the information in dblp).
- When adding a homepage, you need to make sure it can be opened and use a complete http link.

**Step-4**: After all information is modified, push the changes to gitub. The commit information needs to clearly state the purpose of the modification.

**Step-5**: After confirming the modification, you can submit PR on the csrankings website. All PR confirmation information must be confirmed and checked.

**Step-6**: After submitting a PR, you can contact the professor/faculty to send an email to csrankings, stating the PR ID and other information to indicate that it has been submitted; after receiving the PR, the official will review and give a result, which requires timely attention and reply.

## 2. The Listed Faculties and Conference

### 2.1 Listed Faculties
The criteria for inclusion are that anyone who is a full-time, tenure-track faculty
member on a given campus who can solely advise PhD students in **Computer Science** can be included in the database.

### 2.2 Listed Conferences
The ranking ignores journal papers to focus only on conference papers. Only
the very top conferences in each area are listed. All conferences listed must
be roughly equivalent in terms of the number of submissions, selectivity, and
impact to avoid creating incentives to target less selective conferences.

The conferences listed in Table below were developed in consultation with faculty
across a range of institutions, including via community surveys.
Note that **publications must be at least 6 pages long** to be counted.

| **Area**      | **Conference** |
| ----------- | ----------- |
| **AI** | AAAI, IJCAI |
| **CV** | CVPR, ECCV, ICCV |
| **ML Mining** | ICML, ICLR, KDD, NIPS |
| **NLP** | ACL, EMNLP, NAACL |
| **INFORET** | SIGIR, WWW |
| **ARCH** | ASPLOS, ISCA, MICRO, HPCA | 
| **SEC** | CCS, OAKLAND, USENIXSEC, NDSS, PETS | 
| **MOD** | VLDB, SIGMOD, ICDE, PODS |
| **DA** | DAC, ICCAD |
| **BED** | EMSOFT, RTAS, RTSS |
| **HPC** | SC, HPDC, ICS | 
| **Mobile** | MOBICOM, MOBISYS, SENSYS |
| **Metrics** | IMC, SIGMETRICS | 
| **OPS** | OSDI, SOSP, EuroSYS, FAST, USENIXATC |
| **Plan** | POPL, PLDI, OOPSLA, ICFP | 
| **Soft** | FSE, ICSE, ASE, ISSTA | 
| **COMM** | NSDI, SIGCOMM |
| **Graph** | SIGGraph, SIGGraph-Asia, EuroGraphics | 
| **ACT** | FOCS, SODA, STOC |
| **CRYPT** | CRYPTO, EuroCRYPT | 
| **Log** | CAV, LICS |
| **Bio** | ISMB, RECOMB |
| **ECOM** | EC, WINE |
| **CHI** | CHICONF, UBICOMP, UIST |
| **Robotics** | ICRA, IROS, RSS |
| **Visualization** | VIS, VR |
| **CSED** | SIGCSE |

## 3. The Score Calculation Process

### 3.1 Notation
Suppose there are $A$ areas in total. For each institution, suppose that there are
$M$ counted faculties in total.

### 3.2 Faculty Score
A single faculty member gets $1/N$ credit for a paper, where $N$ is the number of
authors, regardless of their affiliation or status (_faculty, student, or otherwise_).
The number never changes. **A paper can count for at most 1 point**, in the case
that all authors are/end up becoming faculty in the database. Each publication
is counted exactly once.

That's to say, if you wrote a paper by yourself and had it published in one of
the designated top conferences in your field, you will get a single point (1 point).
If you wrote a paper with a co-author, then you will each get half a point (1/2
point). You get zero points if you wrote a paper that doesn't appear in a top
conference.

Formally, the score is named as **Adjusted Counts**. For each faculty $m$ in
specific area $a$:

$$(\text{AdjustedCounts}_m)_a = \sum_{i=1}^{K}\frac{1}{N_i}$$

where $K$ is the number of papers for a faculty $m$ published in the listed conferences (as shown in the table above) in specific area $a$, and $N_i$ is the number of co-authors for the $i$-th paper.

### 3.3 Institution Score
For each area $a$, we first calculate the score for the institution by summing up
all the adjusted counts for each faculty, which is given by:
$$(\text{AreaAverageCounts})_a = \sum_{m=1}^{M}(\text{AdjustedCounts}_m)_a$$
Then, we can calculate the **score of the institution** by summing up all the area
scores. Formally, the score for each institution in a specific area is named as
**Average Count**, which is the geometric mean of the adjusted counts per area
for this institution (for $A$ areas selected, this is the $A$-th root of the product of
all adjusted counts $(+1)$).
$$(\text{AverageCount}) =  \sqrt[A]{\prod_{a=1}^{A}((\text{AreaAverageCounts})_a + 1)}$$
_This computation implicitly normalizes publication rates and sizes of areas. An
Institution gets the sum-total of all the points its researchers receive. Currently,
graduate students at the same institution don't get included in the institutional
rankings._

## 4. Frequently Asked Questions

- The professor or faculty homepage information is not aligned. ![](/Fig/Q1.png "Frequently asked question-1.")
- Need to use the full Github homepage link for professor or faculty. ![](/Fig/Q2.png "Frequently asked question-2.")
- The relationship between the professor/faculty’s homepage and the institution/school is not clearly explained. ![](/Fig/Q2.png "Frequently asked question-3.")
- If the professor/faculty information is already in csrankings, to modify the existing professor/faculty information, you need to delete the original information to update it, and it cannot be repeated. ![](/Fig/Q2.png "Frequently asked question-4.")
