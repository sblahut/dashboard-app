<script>
import { Bar } from "vue-chartjs";
import { Chart, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from "chart.js";

Chart.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
    name: "BarChart",
    components: { Bar },
    computed: {
        chartData() {
            const dates = this.chartData.map(d => d.data).reverse();
            const totals = this.chartData.map(d => d.total).reverse();
            return {

                chartData: {
                    labels: dates,
                    datasets: [
                        {
                            label: this.label,
                            backgroundColor: "#f87979",
                            data: totals
                        }
                    ]
                }
            }
        }
    }
};
</script>