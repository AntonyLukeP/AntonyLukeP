<div align="center">

<img src="assets/status-bar.svg" width="100%" alt="status: all systems operational" />

</div>

<br/>

<div align="center">

# SYSTEM.md
### a person, running in production

<img src="assets/topology.svg" width="100%" alt="live system topology — core engineer node connected to Helios, Aegis, AI agent systems, backend services, and full-stack applications" />

</div>

<br/>

## `GET /about`

```
> whoami
software engineering student — backend, distributed systems, AI engineering

> philosophy
tutorials teach you to follow instructions.
production teaches you what breaks, and why.
I build for the second one.
```

I design and ship systems that stay up under conditions nobody planned for — queues that back up, nodes that die mid-request, agents that need to retry without duplicating side effects. The projects below are the evidence.

<br/>

## `GET /services` — active projects

<table>
<tr>
<td width="50%" valign="top">

### `helios` <sup>`● healthy`</sup>
**Durable workflow orchestration engine**

Executes long-running workflows that survive process crashes, deploys, and network partitions. State is checkpointed, not held in memory — kill the worker mid-step and it resumes exactly where it left off.

`Go` `gRPC` `PostgreSQL` `Raft`

[`→ inspect repo`](#)

</td>
<td width="50%" valign="top">

### `aegis` <sup>`● healthy`</sup>
**Distributed observability platform**

Ingests traces, metrics, and logs from a fleet of services and correlates them into a single timeline, so a slow request in one node is traceable back to its root cause in another.

`Rust` `Kafka` `ClickHouse` `gRPC`

[`→ inspect repo`](#)

</td>
</tr>
<tr>
<td width="50%" valign="top">

### `agent-runtime` <sup>`◐ building`</sup>
**Autonomous AI agent systems**

A runtime for agents that plan multi-step tasks, call tools, and recover from failed steps without re-running side effects that already succeeded.

`Python` `LangGraph` `Redis`

[`→ inspect repo`](#)

</td>
<td width="50%" valign="top">

### `full-stack-apps` <sup>`● healthy`</sup>
**Production-grade web applications**

End-to-end apps built the way they'd actually ship — typed APIs, migrations, auth, background jobs, observability from day one, not bolted on after.

`TypeScript` `Next.js` `PostgreSQL`

[`→ inspect repo`](#)

</td>
</tr>
</table>

<br/>

## `GET /timeline` — deploy log

<table>
<tr><td width="110"><code>latest</code></td><td>Shipped <code>aegis</code> trace correlation — cross-service root-cause in under 200ms.</td></tr>
<tr><td><code>-1</code></td><td>Rebuilt <code>helios</code> checkpointing on a Raft-backed log instead of a single Postgres row. Survives leader failover now.</td></tr>
<tr><td><code>-2</code></td><td>First working agent loop that retries a failed tool call without re-sending a payment. Took longer than it should have.</td></tr>
<tr><td><code>-3</code></td><td>Started treating "it works on my machine" as a bug report, not a shrug.</td></tr>
</table>

<br/>

## `GET /runbook` — how I work

<details>
<summary><b>on system design</b></summary>
<br/>

I default to asking what happens when the happy path fails, before I ask what the happy path looks like. Most of the interesting engineering is in the retry, the timeout, and the partial failure — not the first successful request.
</details>

<details>
<summary><b>on stack</b></summary>
<br/>

<img src="https://skillicons.dev/icons?i=go,rust,python,typescript,postgres,redis,kafka,docker,kubernetes,grpc&theme=dark" alt="Go, Rust, Python, TypeScript, PostgreSQL, Redis, Kafka, Docker, Kubernetes, gRPC" />
</details>

<details>
<summary><b>on reading incident reports for fun</b></summary>
<br/>

Yes, actually. The best systems-design education available is free and it's called other companies' public postmortems.
</details>

<br/>

## `GET /metrics` — dashboard

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=YOUR_USERNAME&show_icons=true&hide_border=true&bg_color=0A0E14&title_color=00D9A3&icon_color=00D9A3&text_color=E6EDF3&hide_title=true" height="165" alt="github stats" />
<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=YOUR_USERNAME&layout=compact&hide_border=true&bg_color=0A0E14&title_color=00D9A3&text_color=E6EDF3&langs_count=8" height="165" alt="top languages" />

<img src="https://github-readme-activity-graph.vercel.app/graph?username=YOUR_USERNAME&bg_color=0A0E14&color=E6EDF3&line=00D9A3&point=FFB020&hide_border=true&area=true" width="100%" alt="contribution activity graph" />

</div>

<br/>

<details>
<summary><b>› expand debug console</b></summary>
<br/>

```
$ cat /var/log/why-you-scrolled-this-far.log

[INFO] you read the whole thing. most recruiters spend 6 seconds on a profile.
[INFO] you spent longer than that reading a fake terminal.
[INFO] that curiosity is the whole pitch — it's the same reason I read
       postmortems for fun and reverse-engineer why a retry storm happened
       at 3am instead of just restarting the pod.

$ echo "if you're hiring for backend / distributed systems / AI engineering
        roles, this is usually the point where I'd say 'let's talk.'"

$ status --set-mood
> curious, slightly caffeinated, open to interesting problems.
```

</details>

<br/>

## `POST /contact`

```
{
  "email":    "you@example.com",
  "linkedin": "linkedin.com/in/your-handle",
  "response_time": "< 24h",
  "accepts": ["hard problems", "interesting failures", "collaboration"]
}
```

<div align="center">
<sub>this readme is a running service. see <a href="DESIGN.md">DESIGN.md</a> for the architecture behind it.</sub>
</div>
