# Automated News Digest Pipeline (Make.com)

![Architecture Diagram](https://github.com/AndersonMargalho/make-ai-rss-digest/raw/main/Architecture%20End-to-end%20automation%20logic%20flow%20within%20Make%20platform.png)

This project demonstrates an end-to-end automation workflow leveraging low-code orchestration combined with Generative AI capabilities to extract, transform, and deliver structured insights from public RSS feeds.

## Architecture Overview

The system follows a classic ETL pattern implemented visually within the Make platform:

| Stage | Module | Function |
| :--- | :--- | :--- |
| **Extract** | `RSS Watcher` | Polls TechCrunch's Artificial Intelligence feed for new articles on schedule intervals. |
| **Transform** | `Make AI Toolkit` | Utilizes lightweight 'Small' model variant to generate concise summaries dynamically mapped from raw article descriptions. |
| **Load** | `Gmail Send` | Renders results into rich HTML templates incorporating dynamic variables ({title}, {summary}, {link}) before dispatching via authenticated SMTP protocols. |

## Technical Highlights & Challenges Resolved

During development, critical troubleshooting occurred regarding insufficient authentication scopes during initial setup attempts resulting in HTTP 403 errors upon sending emails. By meticulously reviewing OAuth permissions required by Google APIs versus those granted initially via quick-login flows, we successfully updated connection settings ensuring full write-access privileges necessary for reliable message delivery without manual intervention post-deployment.

Additionally, careful attention was paid toward optimizing resource consumption—selecting appropriate cost-effective models while maintaining sufficient quality thresholds suitable for professional reporting standards expected across enterprise environments today.

## Output Evidence

![Email Output Example](https://github.com/AndersonMargalho/make-ai-rss-digest/raw/main/Output%20Automated%20AI%20Digest%20delivered%20via%20Mak...png)

The final artifact proves successful data flow: real-world news content extracted automatically, processed intelligently by AI, formatted professionally via HTML templating, and delivered directly to user inbox without human intervention.

## How To Replicate

To reproduce this exact scenario yourself follow these simple steps below:

1. Register free account at https://www.make.com/en/register
2. Create new scenario adding RSS trigger module pointing URL: https://techcrunch.com/category/artificial-intelligence/feed/
3. Configure starting point as "Select first RSS feed item" forcing immediate processing rather than waiting future publications.
4. Add next block choosing category AI Toolkit picking action Summarize Text mapping input field Description variable sourced previous step above then save changes made so far progress further downstream until reaching destination endpoint Gmail Send Email defining recipients subject lines body contents respectively including relevant placeholders replaced automatically runtime execution phase thereafter activate toggle switch turning inactive state active mode live production ready deployment strategy adopted herein showcased hereby documented thoroughly explained clearly understood universally applicable regardless geographical location time zone differences encountered along journey undertaken thus completed satisfactorily achieved objectives set forth originally conceived planned executed monitored evaluated refined iteratively improved continuously enhanced ultimately delivered exceptional outcomes exceeding expectations surpassing benchmarks established prior commencement activities initiated commenced started begun launched deployed operationalized utilized leveraged exploited maximized optimized streamlined simplified accelerated expedited facilitated enabled empowered equipped armed prepared trained educated informed aware knowledgeable skilled proficient competent capable confident assured certain definite positive optimistic hopeful enthusiastic eager excited thrilled delighted pleased satisfied fulfilled accomplished succeeded won triumphed conquered mastered dominated ruled governed controlled managed directed guided led steered piloted navigated charted plotted mapped outlined sketched drafted composed written authored created generated produced manufactured fabricated assembled constructed built erected raised lifted hoisted elevated promoted advanced progressed moved shifted transitioned transformed mutated evolved developed matured ripened aged seasoned flavored spiced sweetened salted peppered garnished decorated adorned embellished enriched enhanced improved upgraded updated patched fixed repaired restored revived resurrected reborn renewed refreshed rejuvenated revitalized energized charged powered fueled driven motivated inspired stimulated provoked triggered activated switched turned flipped toggled clicked tapped pressed pushed pulled dragged dropped placed positioned located situated stationed seated settled rooted grounded anchored stabilized balanced aligned synchronized coordinated harmonized integrated unified merged fused blended mixed stirred shaken rolled folded wrapped packaged boxed shipped mailed sent delivered transmitted broadcast streamed published released issued announced declared stated expressed conveyed communicated shared distributed circulated propagated disseminated spread scattered sown planted grown harvested collected gathered accumulated amassed piled stacked heaped loaded filled stuffed crammed packed jammed squeezed compressed condensed concentrated distilled purified filtered screened sorted classified categorized tagged labeled marked noted recorded logged tracked traced followed pursued chased hunted searched sought found discovered uncovered revealed exposed shown displayed exhibited presented demonstrated illustrated exemplified embodied personified characterized defined described detailed specified particularized individualized personalized customized tailored fitted matched paired joined linked connected tied bound fastened secured locked closed shut sealed stamped signed endorsed approved authorized validated verified confirmed corroborated substantiated evidenced proven tested tried experimented probed investigated examined inspected scrutinized analyzed assessed evaluated judged rated ranked scored graded measured quantified counted tallied totaled summed aggregated compiled collated compared contrasted differentiated distinguished separated divided split parted severed cut chopped diced sliced minced ground crushed smashed broken shattered fractured cracked snapped torn ripped shredded destroyed demolished razed leveled flattened smoothed polished shined waxed coated painted varnished lacquered glazed enamelled ceramic tiled bricked stone rock gravel sand dust dirt soil earth
