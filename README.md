# 🌉 Infrastructure Asset Lifecycle Analytics Pipeline

A high-performance data processing pipeline built with `Polars` designed to ingest large-scale structural sensor streams, detect mechanical strain anomalies, and compute asset degradation states for proactive maintenance.

## 📌 Key Capabilities
- **High-Throughput Vectorized ETL:** Leverages `Polars` parallel execution for ultra-fast aggregation and processing of telemetry data streams.
- **Structural Anomaly Detection:** Applies rule-based thresholds on sensor inputs (strain gauges, vibration sensors) to categorize asset risk levels.
- **Lifecycle Health Aggregation:** Computes operational health status indicators across civil infrastructure assets (bridges, tunnels, pavements).

## 📐 System Architecture
```text
[ Sensor Stream Telemetry (Vibration / Strain / Temp) ]
                         │
                         ▼
             ┌──────────────────────┐
             │ Polars High-Speed    │
             │ Data Ingestion Engine│
             └───────────┬──────────┘
                         │
                         ▼
             ┌──────────────────────┐
             │ Parallel Filtering & │
             │ Feature Aggregation  │
             └───────────┬──────────┘
                         │
                         ▼
             ┌──────────────────────┐
             │ Anomaly Evaluator    │
             │ & Health Classifier  │
             └───────────┬──────────┘
                         │
                         ▼
        [ Executive Asset Health Dashboard Feed ]
