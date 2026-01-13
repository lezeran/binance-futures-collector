# Binance Futures Collector

## Overview
This project collects 15-minute USD-M Binance Futures Kline data for the last 365 days for a predefined list of symbols, computes canonical feature sets, and stores the results in Parquet format. The project is designed to run entirely within GitHub Actions, requiring no local machine usage.

## Features
- Uses Binance USD-M Futures REST API.
- Supports robust retry mechanisms and error handling.
- Computes 127 fixed canonical features based on kline data.
- Stores data in Parquet format.
- Generates a summary report with runtime details and skipped symbols.

## File Structure
- `collector/`: Contains main scripts for data collection and API interaction.
- `features/`: Scripts for feature computation.
- `schema/`: Contains the ordered schema for features.
- `data/raw/`: Directory for raw kline data (generated during execution).
- `data/features/`: Directory for computed features (generated).
- `data/run_summary.json`: Summary of the run.
- `.github/workflows/run.yml`: GitHub Actions workflow.

## Installation
To run the project locally:
1. Clone the repository.
2. Create a virtual environment and activate it.
   ```
   python3 -m venv venv
   source venv/bin/activate  # For Windows, use `venv\Scripts\activate`
   ```
3. Install dependencies.
   ```
   pip install -r requirements.txt
   ```

## Usage
### Locally
Run the collection and feature computation:
```bash
python -m collector.run --days 365 --interval 15m --symbols symbols.json
```

### GitHub Actions
The project is configured to run with GitHub Actions. Simply trigger the workflow manually for automated execution.

## Output
- Raw kline data stored in `data/raw/`.
- Computed features saved in `data/features/`.
- Run summary available at `data/run_summary.json`.

## Notes
- Uses Python 3.11.
- The job uses GitHub runner bandwidth, not the user’s mobile data.

## License
This project is licensed under the MIT License.