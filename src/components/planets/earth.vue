<script>
import { Astronomy } from "./calculations/astronomy.js";

export default {
    name: "Earth",
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
            let earthXYZ = Astronomy.Body[3].EclipticCartesianCoordinates(Astronomy.DayValue(new Date()));

            this.x = earthXYZ.x;
            this.y = earthXYZ.y;
            this.z = earthXYZ.z;
        }
    }
    
}
</script>