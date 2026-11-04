# How to Price Art

> They do not teach you this at art school. Everyone is too embarrassed to talk about how much to charge for art.

**Live calculator:** https://grantaj.github.io/how-to-price-art/

A deliberately simple, interactive economics model of the artist's problem: **what size, price and quantity of work should I produce?** The optimisation changes according to your selected objective: expected cash contribution, gross revenue, or number of works sold.

The site is a single dependency-free \`index.html\` served directly from the repository root on GitHub Pages. No build, package install, server, API keys or tracking.

## Model

For each candidate square dimension \`s\`, price \`p\`, and quantity \`n\`, potential purchases during one year are approximated by a Poisson random variable:

\`\`\`text
D ~ Poisson(lambda)
lambda(s,p) = B * M * [appeal(s)/appeal(50)] * [p / P_ref(s)]^(-eta)
P_ref(s)   = P_50 * (s/50)^1.05
appeal(s)  = exp[-0.5 * (ln(s/s_favourite)/0.65)^2]
sold       = E[min(n, D)]
revenue    = p * sold
cash       = (1 - commission) * revenue - n * materials_cost(s)
\`\`\`

The production constraint is \`n * hours_per_work(s) <= available_hours\`. The program exhaustively searches eight candidate square dimensions, 35 price points for each, and feasible production quantities. This is a **single-size annual product strategy**, not an optimisation of a mixed portfolio.

Career stage sets an editable *illustrative* 50 × 50 cm benchmark price. Market conditions multiply the expected demand. The buyer count, demand elasticity, favoured dimensions, studio capacity, per-work materials and time assumptions are editable. Unsold works still incur materials costs. The financial output excludes artist labour costs, GST/tax, rent, framing, marketing, transport and opportunity costs.

**Important:** All initial parameter values are teaching examples, **not** calibrated market data. None of the cited industry sources supplies those numerical model estimates. Calibrate the price benchmark and buyer count using actual comparable sales, and examine sensitivity before taking a result seriously. Maximising numbers sold can perversely recommend low pricing; future career outcomes and price signalling are not represented.

## Sources and context

- [Creative Workplaces — working out fees, payment and pricing](https://creativeworkplaces.gov.au/contracts-and-payment/independent-contractors-artists-and-arts-workers/working-out-fees-payment-and)
- [NAVA Code of Practice — commercial gallery pricing and representation](https://code.visualarts.net.au/selling-and-marketing/commercial-galleries-and-representation/detailed-discussion)
- [NAVA Code of Practice — creative career stages](https://code.visualarts.net.au/payment-rates/how-to-use-payment-standards/creative-career-stages)
- [Art Basel & UBS Global Art Market Report 2026](https://www.artbasel.com/news/the-art-basel-and-ubs-global-art-market-report-2026)

Possible research extensions: optimise a *mixture* of sizes, model scarcity and price signalling, infer demand from actual sales histories (including censored stockouts), introduce repeat collectors and longer-horizon career value, and quantify parameter uncertainty.
