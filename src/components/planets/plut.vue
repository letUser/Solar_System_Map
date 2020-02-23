<script>
import { Astronomy } from "./calculations/astronomy.js";

export default {
    name: "Plut",
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
            let plutXYZ = Astronomy.Body[20].EclipticCartesianCoordinates(Astronomy.DayValue(new Date()));

            this.x = plutXYZ.x;
            this.y = plutXYZ.y;
            this.z = plutXYZ.z;
        }
    }
    
}
</script>