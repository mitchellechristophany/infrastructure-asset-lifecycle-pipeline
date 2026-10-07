import numpy as np
import polars as pl

# Generate Mock Sensor Streams from Infrastructure Assets (e.g., Bridges/Pavements)
n_rows = 50000
data = pl.DataFrame(
    {
        "asset_id": np.random.choice(
            ["Bridge_01", "Bridge_02", "Tunnel_A", "Tunnel_B"], n_rows
        ),
        "vibration_hz": np.random.normal(50.0, 10.0, n_rows),
        "strain_gauge_val": np.random.uniform(100.0, 500.0, n_rows),
        "temperature_c": np.random.uniform(-10.0, 45.0, n_rows),
    }
)

# High-Performance Data Transformation using Polars
processed = (
    data.filter(pl.col("temperature_c") > 0)
    .group_by("asset_id")
    .agg(
        [
            pl.col("vibration_hz").mean().alias("avg_vibration"),
            pl.col("strain_gauge_val").max().alias("max_strain"),
            pl.col("vibration_hz").count().alias("reading_count"),
        ]
    )
    .with_columns(
        pl.when(pl.col("max_strain") > 450.0)
        .then(pl.lit("CRITICAL"))
        .otherwise(pl.lit("NORMAL"))
        .alias("health_status")
    )
)

print(processed)
