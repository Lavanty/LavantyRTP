# LavantyRTP
Simple /rtp plugin that you can use on your server you can do /rtp and chose betwen overworld nether and end have fun and if any1 needs help dm me on discord lavanty

import org.bukkit.command.Command;
import org.bukkit.command.CommandExecutor;
import org.bukkit.command.CommandSender;
import org.bukkit.ChatColor;
import org.bukkit.Location;

import java.util.concurrent.ThreadLocalRandom;

public class RTPCommand implements CommandExecutor {
    @Override
    public boolean onCommand(CommandSender sender, Command cmd, String label, String[] args) {
        if (args.length == 1) {
            String dimension = args[0].toLowerCase();

            if (dimension.equals("overworld") || dimension.equals("nether") || dimension.equals("end")) {
                int maxCoordinate = getMaxCoordinate(dimension);
                int x = ThreadLocalRandom.current().nextInt(-maxCoordinate, maxCoordinate);
                int z = ThreadLocalRandom.current().nextInt(-maxCoordinate, maxCoordinate);
                int y = sender.getWorld().getHighestBlockYAt(x, z);
                Location randomLocation = new Location(sender.getWorld(), x, y, z);

                sender.teleport(randomLocation);
            } else {
                sender.sendMessage(ChatColor.RED + "Invalid dimension. Use: overworld, nether, or end.");
            }
        } else {
            sender.sendMessage(ChatColor.RED + "Usage: /rtp <dimension>");
        }

        return true;
    }

    private int getMaxCoordinate(String dimension) {
        switch (dimension) {
            case "nether":
                return 128;
            case "end":
                return 10000;
            default:
                return 30000;
        }
    }
}

