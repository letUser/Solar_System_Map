<script>
import { Astronomy } from "./calculations/astronomy.js";

export default {
    name: "Sat",
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
            let satXYZ = Astronomy.Body[17].EclipticCartesianCoordinates(Astronomy.DayValue(new Date()));

            this.x = satXYZ.x;
            this.y = satXYZ.y;
            this.z = satXYZ.z;
        }
    }
    
}
</script>