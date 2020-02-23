<script>
import { Astronomy } from "./calculations/astronomy.js";

export default {
    name: "Ven",
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
            let venXYZ = Astronomy.Body[2].EclipticCartesianCoordinates(Astronomy.DayValue(new Date()));

            this.x = venXYZ.x;
            this.y = venXYZ.y;
            this.z = venXYZ.z;
        }
    }
    
}
</script>