# Veichi-Financial-Sizing-Saving-Combined


### Overview

This Python script calculates the annual financial savings of a solar-powered water pump system using Veichi drives. It integrates solar irradiance, pump characteristics, climate adjustments, and energy tariffs to simulate realistic monthly performance and estimate cost savings.

### Structure

#### 1. Merged Input Section

Defines all system parameters and input data in one consolidated block:

* `actual_kwh`: Monthly utility energy consumption (kWh).
* `days_per_month`: Calendar days per month.
* `climate_index_h`: Monthly climate adjustment factors.
* `motor_kw`, `solar_kw`: Pump motor size and solar array size (in kW).
* `drive_min_pct`: Minimum drive output required for operation (as a decimal).
* `kwh_cost`: Cost of electricity per kWh.
* `loss_factor_hourly`, `loss_factor_monthly`: Efficiency loss factors for hourly yield and monthly savings, respectively.

#### 2. Pump Hours Calculation

Computes the number of daily pumping hours per month:

```
pump_hours_per_day = (monthly_kwh / days_in_month) / motor_kw
```

#### 3. Hourly Yield Simulation

Using a symmetric distribution function (`build_excel_matched_distribution_fixed()`), this section:

* Distributes available pump hours around midday (12:00) to simulate solar performance.
* Applies a solar power curve to derive effective yield.
* Outputs an estimated daily energy yield (`hourly_yield_j`) for each month.

Additionally, the script prints the 13-hour spread used for each month for validation.

#### 4. Monthly Financial Calculation

Uses the hourly yields to compute:

* Adjusted yield using climate index.
* Theoretical savings based on full output.
* Capped savings limited to actual utility expenditure.
* Final savings after applying the efficiency loss factor.

#### 5. Output

Prints a structured table showing:

* Monthly pump hours
* Daily yield
* Adjusted yield with climate
* Monthly energy expenditure
* Theoretical, capped, and actual savings
* Total actual savings across the year

---

### Notes

* This implementation uses a simplified drive model and symmetrical hour distribution. Real-world results may vary based on actual irradiance profiles, panel orientation, and site-specific factors.
* The spread function does not account for real irradiance data by hour. To improve accuracy, replace it with empirical hourly profiles per month.


