# DEVX-080: AWS Emulator: let agents test against a local fake AWS instead of your account

## Summary

AWS released an official local emulator of the AWS APIs (no account, no fees) with an agent skill that installs it, points CLI/SDK at it and fixes cert/signing errors. Agents run aws/boto3 against a sandbox endpoint with throwaway keys instead of near real credentials. In-memory (resources vanish on stop); its docs say not to use it to test security. Feasibility High, stage Trial, ~20 min. 803 points on HN.

## Details

- PoC: build the 6-line Dockerfile from the Docker guide, run `docker run --rm --memory=2g -p 127.0.0.1:9297:9297 ... aws-emulator -p 9297 --telemetry off`, then in a second shell unset real AWS creds, export AWS_ENDPOINT_URL=https://127.0.0.1:9297 plus the emulator credentials/config/CA bundle paths, and check `aws sts get-caller-identity` returns account 000000000000 (full commands below).
- Or let the agent do it: `aws agent-toolkit add-skill --skill-name aws-emulator --region us-east-1` (AWS CLI 2.35.0+).
- Caveats: telemetry on by default; bind to 127.0.0.1 only; Terraform support not verified, check per-service fidelity scores on the releases page.
- Success metric: share of agent test runs touching real AWS (target zero), minutes saved per infra test cycle.
- Health: CC0, ~3k stars, created Sept 2026, run by AWS, no PRs accepted, multiple releases a day. Seen in 4 sources. Expires Feb 10, 2027.
- Methods review (Nov 12): agents built and tested the emulator from more than 400 Smithy models in three teams (one writes tests, one finds gaps, one fixes). The pattern: first the agent fixes a fidelity test until it passes against real AWS, then it builds the emulator until it passes that same test; above that sits a merge gate with attacking security agents—a spec, a real source of truth, and a gate, at product scale rather than a demo. Open source, about 29.7k commits in three weeks, and a public folder of known gaps named `things-that-do-not-work`. An IDC analyst notes it has no throttling, no fault simulation, and no regional differences. Amazon's claim that no human reviewed the code is a statement only. 814 points on HN (803 at an earlier count). Scores: effectiveness 4/5, hype 3/5. Fit: high as an engineering pattern for any team building agents, because it is a clear definition of how to verify an agent's work; the emulator itself is also a cheap test environment for agents that touch AWS. Effort: low to use, medium to adopt the pattern. Recommendation: Adopt for the pattern. Continues the verification line from Nov 5, where OpenAI showed you need to verify the path, not only the result.

## Content

### 2. AWS Emulator: let agents test against fake AWS, not your account — Enterprise feasibility: High | Stage: Trial

- What changed: AWS released an official local emulator of the AWS APIs (no account, no fees). It ships an agent skill that installs it, points your CLI/SDK at it, and fixes cert/signing errors. It hit 803 points on HN.
- Why it matters: agents run `aws`/boto3 against a sandbox endpoint with throwaway keys, instead of near real credentials. It's in-memory (resources vanish on stop), and its docs say not to use it to test security.
- Effort: ~20 min (Docker build on macOS/Windows, package on Linux).
- PoC: build the 6-line Dockerfile from the [Docker guide](https://docs.aws.amazon.com/emulator/latest/userguide/getting-started-docker.html), then:

```bash
docker run --rm --memory=2g -p 127.0.0.1:9297:9297 -e HOME="$HOME" \
  -v "$HOME/.aws/emulator:$HOME/.aws/emulator" aws-emulator -p 9297 --telemetry off
# second shell:
unset AWS_ACCESS_KEY_ID AWS_SECRET_ACCESS_KEY AWS_SESSION_TOKEN AWS_PROFILE
export AWS_ENDPOINT_URL=https://127.0.0.1:9297 AWS_REGION=us-east-1 \
  AWS_SHARED_CREDENTIALS_FILE=~/.aws/emulator/9297/emulator_credentials \
  AWS_CONFIG_FILE=~/.aws/emulator/9297/config AWS_CA_BUNDLE=~/.aws/emulator/9297/ca.pem \
  AWS_EC2_METADATA_DISABLED=true AWS_DISABLE_HOST_PREFIX_INJECTION=true
aws sts get-caller-identity   # Account must be 000000000000
```

  Or let the agent do it: `aws agent-toolkit add-skill --skill-name aws-emulator --region us-east-1` (needs AWS CLI 2.35.0+).
- Caveats: telemetry is on by default (`--telemetry off` above). Bind to `127.0.0.1` only, as shown. Terraform support was not verified; check the per-service fidelity scores on the releases page first.
- Success metric: share of agent test runs that touch real AWS (target: zero), and minutes saved per infra test cycle.
- Health: CC0 license, about 3k stars, created Sept 2026, run by AWS, doesn't accept PRs, multiple releases a day.
- Sources: [repo](https://github.com/aws/aws-emulator), [HN thread](https://news.ycombinator.com/item?id=50456631), [Simon Willison](https://simonwillison.net/2026/Nov/11/aws-emulator/), [Werner Vogels' blog](https://www.allthingsdistributed.com/2026/11/aws-emulator-and-the-engineers-job-when-agents-write-the-code.html) | seen in 4 sources | expires Feb 10, 2027

## Sources

- [aws/aws-emulator repo](https://github.com/aws/aws-emulator)
- [Docker guide](https://docs.aws.amazon.com/emulator/latest/userguide/getting-started-docker.html)
- [HN thread](https://news.ycombinator.com/item?id=50456631)
- [Simon Willison](https://simonwillison.net/2026/Nov/11/aws-emulator/)
- [Werner Vogels' blog](https://www.allthingsdistributed.com/2026/11/aws-emulator-and-the-engineers-job-when-agents-write-the-code.html)
- [AWS Emulator announcement](https://aws.amazon.com/blogs/aws/test-your-applications-against-aws-locally-with-aws-emulator/)
