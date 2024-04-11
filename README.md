<h1 align="center">SolasAI Disparity and Bias Testing Library</hq>

<h3 align="center" style="font-weight:300">
A Python Library of Curated Disparity Testing Metrics for Use in Real-World Settings
</h1>

<div align="center">
<br>
<img alt="SolasAI banner" src="https://raw.githubusercontent.com/SolasAI/solas-ai-disparity/main/images/SolasAI-Logo.png"/>
<br><br>
</div>

<div align="center">
<i>This text and associated software do not represent and should not be construed as providing legal advice or requirements for regulatory compliance.</i>
</div>

## About the SolasAI Disparity and Bias Testing Lbrary

The SolasAI Disparity Testing Library is a collection of tools that allows modelers, compliance, and business stakeholders to test outcomes for bias or discrimination using widely accepted fairness metrics.

See also:

* Our [detailed example notebooks](https://github.com/SolasAI/solas-ai-disparity/tree/main/examples)
* Our [API documentation](https://solasai.github.io/solas-ai/)

## Example usage: Calculating an adverse impact ratio

```python
import solas_disparity as sd

air_disparity = sd.adverse_impact_ratio(
    group_data=df,
    protected_groups=['black', 'hispanic', 'asian', 'female'],
    reference_groups=['white', 'white', 'white', 'male'],
    group_categories=['race', 'race', 'race', 'sex'],
    outcome=df['Approved'],
    sample_weight=None,
    air_threshold=0.90,
    percent_difference_threshold=0.0,
)
```

For more detailed examples, please refer to our [example notebooks](https://github.com/SolasAI/solas-ai-disparity/tree/main/examples)

### Additional metrics included with SolasAI's Disparity Testing Library

- Adverse Impact Ratio (AIR)
- By-Quantile Adverse Impact Ratio
- Categorical Adverse Impact Ratio
- Custom Disparity Metric
- False Discovery Rate
- False Negative Rate
- False Positive Rate
- Odds Ratio
- Precision
- Residual Standardized Mean Difference
- Scoring Impact Ratio
- Segmented Adverse Impact Ratio
- Selection Impact Ratio
- Standardized Mean Difference (SMD)
- True Negative Rate
- True Positive Rate

Additional metrics are coming soon, including a generic customizable disparity testing function, which can create a disparity measurement from nearly any `scikit-learn`-style metric.

## Installation<a name="Install"></a>

```bash
pip install solas-ai
```

To run the example notebooks in this repository, also install the following:

```bash
pip install notebook xgboost scikit-learn
```

SolasAI is supported on Python 3.7 through 3.11, on Windows, MacOS, and Linux.

## Why SolasAI?

There are many good open-source disparity testing libraries already available (we encourage you to try them!).  So why use SolasAI's Library?

SolasAI's disparity testing library was built by industry practitioners with decades of experience in fair lending, employment discrimination analysis,
and algorithmic compliance. The methodologies included in this library are widely used across the fairness analytics space and were created
to align with legal and regulatory expectations. For example, the Adverse Impact Ratio
is [cited by the EEOC](https://www.eeoc.gov/laws/guidance/questions-and-answers-clarify-and-provide-common-interpretation-uniform-guidelines#:~:text=Adverse%20impact%20is%20normally%20indicated,numbers%20of%20selections%20are%20made.)
as a standard metric for evaluating disparities in employment decisions.

Because of our experience in the field, we built SolasAI and this disparity testing library to solve common challenges that many users will face. Using the United States as an example, outside of mortgage lending, lenders generally do not have access to race/ethnicity data and will rely on proxy methodologies like the [Bayesian Improved Surname Geocoding (BISG)](https://github.com/cfpb/proxy-methodology) method to predict probabilities of demographic membership. Other libraries require binary (0/1) demographic membership for testing (ex. "Black" or "White"), which is unfortunate since converting BISG probabilities to fit that format results in substantial loss of information. SolasAI's disparity testing library accommodates binary or continuous demographic probabilities, making it compatible with self-reported or proxied values with no changes in functionality.

In addition to standard metrics like the Adverse Impact Ratio (AIR) and Standardized Mean Difference (SMD), other metrics extend on the AIR or SMD to better solve real-world use cases. Some are more straightforward: the Categorical AIR, for example, allows for disparity calculations on rankable categorical outcomes instead of just binary outcomes. Others involve more sophisticated methodological changes. The Segmented AIR allows a user to account for differences in underlying demographics across some segment (ex. State, product type) and then uses a Cochran-Mantel-Haenszel test to determine the statistical significance of any remaining disparity.

Other examples of enhancements include:
- Customizable practical significance thresholds
- Compatibility with sample weights
