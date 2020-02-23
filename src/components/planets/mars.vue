<script>
import { Astronomy } from "./calculations/astronomy.js";

export default {
    name: "Mars",
    props: {},
    data() {
        return {
            x: 0,
            y: 0,
            z: 0,

        };
    },
    methods: {
        takeGEO: function() {
            let marsXYZ = Astronomy.Body[5].EclipticCartesianCoordinates(Astronomy.DayValue(new Date()));

            this.x = marsXYZ.x;
            this.y = marsXYZ.y;
            this.z = marsXYZ.z;
        }
    }
    
}
</script>