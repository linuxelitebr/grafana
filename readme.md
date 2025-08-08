# OCP Virt HCP - Metrics Dashboard

## Overview

This Grafana dashboard provides comprehensive monitoring for OpenShift Virtualization (KubeVirt) environments, offering real-time insights into virtual machine performance, resource consumption, and cluster health metrics.

It also supports OpenShift Hosted Clusters.

## Purpose

Monitor and analyze the health and performance of virtualized workloads running on OpenShift Container Platform with KubeVirt, providing visibility into:
- Virtual Machine Instance (VMI) lifecycle and states
- Resource consumption patterns
- Node utilization
- API server performance

## Dashboard Panels

### System Overview
- **VM Running**: Current count of running virtual machines
- **Allocatable Nodes**: Total number of nodes available for VM scheduling

### VMI Lifecycle Monitoring
- **VMI by Phase**: Time-series visualization of VMI states (scheduling, scheduled, running, success)
- **VMI Running by Nodes**: Distribution of running VMIs across cluster nodes
- **VMI by OS**: Breakdown of VMIs by operating system
- **VMI by Flavor**: Distribution based on VM performance profiles

### Resource Utilization
- **Agent Nodes CPU**: CPU utilization across compute nodes
- **Agent Nodes Load**: System load average monitoring

### Top Consumers Analysis
- **Top Consumers of CPU**: Top 10 VMs by CPU usage rate
- **Top Consumers of Memory**: Top 10 VMs by memory consumption
- **Top Consumers of Storage IOPS**: Top 5 VMs by I/O operations
- **Top Consumers of Storage Traffic**: Top 5 VMs by storage throughput

### Network Monitoring
- **Network Traffic by Virtual Machines**: Network bandwidth usage per VM

### Performance Metrics
- **VMI Scheduling Time**: 95th percentile of VM scheduling latency
- **API Server - Read Request Duration**: GET/LIST/WATCH operation latencies
- **API Server - Write Request Duration**: POST/PUT/PATCH/DELETE operation latencies

## Requirements

### Prerequisites
- Grafana Operator 5.18.0 or higher
- Prometheus data source configured
- KubeVirt metrics exposed via Prometheus

### Required Metrics
The dashboard requires the following KubeVirt metrics:
- `kubevirt_vmi_*` (VMI metrics)
- `kubevirt_allocatable_nodes`
- `container_cpu_usage_seconds_total`
- `node_cpu_seconds_total`
- `node_load1`
- `apiserver_request_duration_seconds_bucket`

## Installation

1. **Import Dashboard**:
   - Navigate to Grafana > Dashboards > Import
   - Upload the `ocp-virt-hcp.json` file or paste the JSON content
   - Select your Prometheus data source

2. **Configure Data Source**:
   - The dashboard uses a variable `${datasource}` for the Prometheus data source
   - Ensure your Prometheus instance is properly configured and collecting KubeVirt metrics

## Configuration

### Time Range
- Default: Last 15 minutes
- Auto-refresh: Every 5 seconds

### Variables
- **datasource**: Prometheus data source (hidden variable, auto-configured)

## Dashboard Details

- **Dashboard ID**: 3
- **UID**: `feuedi6hm3a4gf`
- **Version**: 14
- **Schema Version**: 40

## Visualization Types

The dashboard utilizes various Grafana visualization panels:
- **Stat Panels**: For single value metrics
- **Time Series**: For historical data trends
- **Bar Gauge**: For OS distribution
- **Gauge**: For flavor distribution

## Notes

### Annotations
- Dashboard includes annotation support for marking significant events
- Configured to display Grafana system annotations

### Performance Considerations
- Uses logarithmic scale for better visualization of metrics with wide value ranges
- Implements 5-minute, 30-minute, and custom time windows for different metric calculations
- Top consumer panels limited to top 5-10 entries to maintain dashboard performance

### Known Limitations
- OS and Flavor metrics depend on proper VMI annotations
- Some metrics may show as "approximate values" if VMIs lack required metadata

## Contributing

When modifying this dashboard:
1. Export the dashboard JSON after making changes
2. Update the version number in the JSON
3. Document any new metrics or panels in this README
4. Test with different time ranges and data volumes

## License

This dashboard configuration is provided as-is for monitoring OpenShift Virtualization environments.

## Related Resources

- [KubeVirt Documentation](https://kubevirt.io/)
- [OpenShift Virtualization](https://www.openshift.com/learn/topics/virtualization)
- [Prometheus Operator](https://github.com/prometheus-operator/prometheus-operator)
- [Grafana Documentation](https://grafana.com/docs/)

## Support

For issues or questions regarding this dashboard:
1. Check the Prometheus targets to ensure metrics are being collected
2. Verify KubeVirt components are properly instrumented
3. Review Grafana query inspector for troubleshooting panel queries

---

**Last Updated**: Dashboard Version 14
**Compatibility**: OpenShift 4.18 with KubeVirt/OpenShift Virtualization
